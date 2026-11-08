---
description: Accepted collateral assets, valuation and withdrawal checks
---

# 🏋️ Collateral

Borrowing on the Fixed-Rate Lending Protocol requires **over-collateralization**: you deposit assets worth more than you borrow. If collateral no longer sufficiently covers the debt, the position can be [liquidated](liquidation/).

## Supported assets by network

| Network            | Lend / Borrow                 | Accepted as collateral       |
| ------------------ | ----------------------------- | ---------------------------- |
| **Ethereum**       | WBTC, ETH, USDC, axlFIL, JPYC | WBTC, ETH, USDC, JPYC, uMINT |
| **Arbitrum**       | WBTC, ETH, USDC               | WBTC, ETH, USDC              |
| **Filecoin (FVM)** | FIL, USDFC                    | FIL, iFIL, wpFIL, USDFC      |

{% hint style="info" %}
Select your network in the app to see available markets and accepted collateral.
{% endhint %}

{% hint style="warning" %}
Avalanche support is **deprecated**. Polygon zkEVM has been **sunset and is no longer operational**. Legacy deployment addresses are retained for historical reference only: [Contracts & Security](../contracts-and-security/).
{% endhint %}

For reference haircuts and liquidation thresholds, see [Protocol Parameters](../protocol-parameters.md).

## Asset notes

* **USDFC** — Secured Finance's own FIL-backed stablecoin, minted via CDP on FVM. [Learn more](../../usdfc-stablecoin/overview.md).
* **iFIL / wpFIL (liquid staking tokens)** — represent staked FIL that keeps earning staking rewards _while_ serving as collateral. For example, stake FIL on [GLIF](https://glif.io/) to receive iFIL, then deposit the iFIL as collateral — a dual-yield position. Both are accepted on Filecoin.
* **axlFIL** — Axelar-bridged FIL on Ethereum.
* **JPYC** — JPY-pegged stablecoin; fixed-rate JPY lending markets are live on **Ethereum**.
* **RWA collateral** — tokenized money-market fund collateral (uMINT, via DigiFT), accepted as collateral on **Ethereum**.

## How collateral is monitored

* The protocol values assets using the **price feeds configured for each currency on the selected network**, plus [Mark-to-Market](liquidation/mark-to-market.md) pricing for ZC bond positions.
* Loan-to-Value (LTV) is debt value divided by collateral value. In [Portfolio](../getting-started/platform-guide/portfolio.md), monitor Collateral Utilization and Liquidation Risk. [Managing Your Positions](../getting-started/managing-positions.md) explains these app indicators.
* If LTV rises above the liquidation threshold, the position can be [liquidated](liquidation/).

**Multi-collateral is supported**: you can back a single borrowing book with several asset types, diversifying against any one asset's volatility.

## Price sources and verification

Collateral and debt are valued using price feeds selected for each asset and network. This applies on Ethereum, Arbitrum and Filecoin. Some assets combine several feeds or use a fixed value instead of a market price.

For example, borrowing USDC against ETH on Ethereum or Arbitrum depends on both assets' prices. ZC bond positions also use [Mark to Market](liquidation/mark-to-market.md) pricing.

{% hint style="warning" %}
Protocol values may differ from sale prices. For example, Filecoin USDFC uses a [fixed $1 value](collateral.md#filecoin-usdfc-fixed-valuation), so a fall in its market price alone does not reduce its protocol value. Account risk depends on the collateral and debt mix. Monitor market liquidity alongside Collateral Utilization and Liquidation Risk.
{% endhint %}

**For developers**

<details>

<summary>How to check feeds on Ethereum, Arbitrum or Filecoin</summary>

Use the CurrencyController address for the intended network from [Contracts & Security](../contracts-and-security/). Ethereum, Arbitrum and Filecoin have separate configurations, even where contract addresses match. Read getCurrencies(), then getPriceFeed(currency) with the relevant bytes32 currency key, and check every returned feed. Use getLastPrice(currency) to read the combined result.

A [Chainlink-compatible interface](https://github.com/Secured-Finance/contracts/blob/62072571fd22a882a622b587eeefffc83efbb199/contracts/protocol/CurrencyController.sol) does not identify the feed operator. Inspect the underlying source, any token-conversion adapters and the heartbeat settings. The controller rejects non-positive answers and answers whose reported timestamps are older than the configured heartbeat plus its buffer.

Inspect the deployed configuration on the selected network; feed routes can change independently across networks.

The documented Filecoin routes are:

| Asset | Valuation route                         |
| ----- | --------------------------------------- |
| FIL   | RedStone FIL/USD                        |
| iFIL  | iFIL/FIL conversion × RedStone FIL/USD  |
| wpFIL | wpFIL/FIL conversion × RedStone FIL/USD |

For the migration from Pyth, execution references and dated on-chain verification, see [Contract Upgrade History](../contracts-and-security/contract-upgrade-history.md).

</details>

<details>

<summary>Filecoin USDFC: fixed valuation</summary>

The fixed $1 reference reduces the lending valuation's sensitivity to thin-pool price swings and manipulation. [Redemption](../../usdfc-stablecoin/core-mechanics/redemption.md) in the separate stablecoin protocol cancels nominal debt at $1 per USDFC redeemed; FIL received depends on the oracle price, fees and execution conditions. Profitable redemption can support the peg, while market liquidity and sale proceeds can still differ from the protocol value.

This lending conversion is separate from a ZC bond's [Mark Price](liquidation/mark-to-market.md) and the [stablecoin protocol](../../usdfc-stablecoin/overview.md)'s collateral oracle.

The configured [StaticPriceAggregator](https://filfox.info/en/address/0x8aa14976161882e6853FAa93fB89324464aed8f1) returns 100000000 with 8 decimals. [Its timestamp](https://github.com/Secured-Finance/contracts/blob/62072571fd22a882a622b587eeefffc83efbb199/contracts/external/oracles/StaticPriceAggregator.sol) is the current block time, not a new market-price observation. See [Contract Upgrade History](../contracts-and-security/contract-upgrade-history.md) for the on-chain verification record.

</details>

## Common questions

<details>

<summary>What happens if my collateral value drops?</summary>

Your LTV rises. Above the liquidation threshold, up to 50% of your debt can be liquidated, or up to **100%** past the full-liquidation threshold, with a fee taken from your collateral. Reduce risk early by adding collateral or executing a trade to reduce the debt. See [Liquidation](liquidation/).

</details>

<details>

<summary>Can I withdraw collateral while I have open borrows?</summary>

Yes, up to the amount allowed by the current collateral and withdrawal checks. Review the available amount and risk indicators before confirming. Keep a collateral buffer, because asset prices can change after withdrawal.

</details>

<details>

<summary>Can ZC bonds themselves be used as collateral?</summary>

Yes — lending positions can serve as collateral for borrowing in the same currency, enabling yield-spread strategies. See [ZC Bonds as Collateral](zc-bonds-as-collateral.md).

</details>
