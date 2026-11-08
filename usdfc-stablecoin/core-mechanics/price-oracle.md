---
description: Where the FIL/USD price comes from and what happens when it goes stale
---

# 🔮 Price Oracle

Every collateral ratio in the protocol — and therefore every liquidation and redemption — depends on one number: the FIL/USD price reported by the **PriceFeed** contract. This page explains where that price comes from and how the protocol behaves when it can't get a fresh one.

## Checking oracle status in the app

1. In the [USDFC app](https://app.usdfc.net), open **Dashboard → Protocol Overview** for the displayed FIL price and RedStone/Tellor source links. This overview does not display a freshness timestamp; check the Trove page for action restrictions.
2. Open the **Trove** page and read any price warning above the form:
   * **“Market price data has not been updated…”** or **“We're unable to verify the current market price…”** means Trove actions are unavailable.
   * **“We're temporarily unable to fully verify the latest market price…”** means opening, additional borrowing and collateral withdrawal are unavailable. Adding collateral, repaying or closing still depend on the mode-specific rules and other checks below; closure is blocked in Recovery Mode.
3. If a price warning blocks your action, wait for it to clear and review the form again. If the app cannot load a price status, do not submit until it can. The transaction uses the on-chain state at execution, which may differ from the displayed quote.

The warning wording is documented in the [app's price-warning component](https://github.com/Secured-Finance/stablecoin-app/blob/d12f67fb6164ab8a653f28fec2faeeecac01fed0/src/components/Trove/PriceSourceWarning.tsx). Developers can read source and freshness together with the [SDK's oracle-aware monitoring example](../../developer-portal/sdk-reference/usdfc-sdk.md#monitoring-liquidation-risk).

## The two price sources

| Role     | Source                                | Notes                                                          |
| -------- | ------------------------------------- | -------------------------------------------------------------- |
| Primary  | [RedStone](https://redstone.finance/) | Chainlink-compatible FIL/USD price feed; replaced Pyth in 2026 |
| Fallback | [Tellor](https://tellor.io/)          | Decentralized oracle network; updated roughly every 12 hours   |

Tellor's fallback updates are submitted roughly every 12 hours by a Secured Finance-operated job. This creates an operational dependency on the team, even though Tellor is a decentralized oracle network.

## When the protocol switches sources

PriceFeed normally uses RedStone. If that feed times out or returns invalid data, it can switch to a valid, fresh Tellor price. If neither source is usable, it uses the last good price within the 48-hour limit below.

RedStone is treated as unavailable when:

* The primary price hasn't been updated for longer than the **oracle timeout (16 hours)**
* The primary call reverts, or returns invalid data or an invalid timestamp

A large price move receives an extra check: while the primary feed is working normally, a price more than double or less than half the last good price is accepted only if a live, valid Tellor price agrees within 5%. Otherwise, PriceFeed keeps the last good price rather than adopting the conflicting quote.

Recovery depends on why the feed switched. If the primary was marked untrusted, both feeds must be live, valid and within 5% to restore it. If the primary only timed out, it can also return when it is live and Tellor is invalid. If Tellor is merely stale, PriceFeed keeps the last good price; if both live feeds disagree, it continues with Tellor. A responding primary feed alone therefore does not always restore borrowing.

## When both sources are stale

When neither oracle provides a usable price, the protocol can temporarily use its last accepted price ("last good price") for up to **48 hours**. During that time, opening a Trove, borrowing more and withdrawing collateral remain blocked because they require the primary oracle.

**After that limit**, if there is still no usable oracle price, price-dependent transactions stop until one becomes available. This includes adding collateral, repaying debt, closing a Trove, liquidations and redemptions. The app may still display the old price.

<details>

<summary>How is the 48-hour limit measured?</summary>

The clock starts when PriceFeed stores an accepted value, not when the oracle originally observed the market price. The underlying observation can therefore be older than 48 hours.

</details>

## Which actions remain available?

Opening a Trove, borrowing more USDFC or withdrawing FIL requires an accepted price from the primary oracle. Other actions can use an accepted fallback or last good price while it remains within its time limit. The table shows the oracle requirement for each action.

| Action                                                           | Current primary price | Accepted fallback or last good price within its freshness limit | No usable transaction price |
| ---------------------------------------------------------------- | --------------------- | --------------------------------------------------------------- | --------------------------- |
| Open a Trove                                                     | Available\*           | Blocked                                                         | Blocked                     |
| Increase debt, including when adding collateral at the same time | Available\*           | Blocked                                                         | Blocked                     |
| Withdraw collateral, including when repaying at the same time    | Available\*           | Blocked                                                         | Blocked                     |
| Add collateral without increasing debt or withdrawing collateral | Available\*           | Available\*                                                     | Blocked                     |
| Repay debt without increasing debt or withdrawing collateral     | Available\*           | Available\*                                                     | Blocked                     |
| Close a Trove                                                    | Available\*           | Available\*                                                     | Blocked                     |
| Liquidate or redeem                                              | Available\*           | Available\*                                                     | Blocked                     |

\* Available means the oracle permits the action. All other protocol checks still apply: partial repayment must leave at least 200 USDFC of net debt (excluding the 20 USDFC Liquidation Reserve); Recovery Mode blocks closure; liquidation and redemption require their own eligibility checks. See Recovery Mode for the borrower ratio rules.

When combining actions, any new borrowing or collateral withdrawal makes the whole transaction require the primary oracle. This includes borrowing while adding FIL, or withdrawing FIL while repaying debt.

For a Trove owner, the practical implication: during an oracle outage the price the protocol uses can lag the real market. A liquidation that "should" have happened may be delayed — and conversely, you cannot assume a market recovery protects you until the on-chain price reflects it.

Upgrade history: these primary-oracle requirements were introduced in the [30 October 2026 upgrade](../deployed-contracts/contract-upgrade-history.md).

## Where next

* [Liquidation](liquidation.md) — how the oracle price triggers liquidations
* [Contracts and Security](../deployed-contracts/) — contract addresses
