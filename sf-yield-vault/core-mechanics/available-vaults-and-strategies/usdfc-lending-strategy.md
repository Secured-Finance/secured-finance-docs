---
description: Automated, rule-based USDFC lending into Fixed-Rate Lending markets
---

# 💲 USDFC Lending Strategy

## Overview

The **USDFC Lending Strategy** is the strategy deployed within the [**USDFC Vault**](https://vaults.secured.finance/314/0x9f59bB0A1dbfad10443Fba08D41c75b0664Bf41B) under the Secured Finance framework.

This strategy is designed to generate yield by deploying **USDFC** into the Secured Finance fixed-rate lending markets on Filecoin, allowing Vault participants to earn variable returns without actively managing positions.

The strategy is **fully rule-based**: every rule described on this page is encoded in the deployed strategy contract, which can be inspected on-chain directly from the Vault page.

| | |
| --- | --- |
| Base asset | [USDFC](../../../usdfc-stablecoin/overview.md) |
| Network | Filecoin |
| Strategy contract | **Secured Finance USDFC Lender** — see [Contracts and Security](../../contracts-and-security.md) |
| Vault share token | yvUSDFC |
| Yield type | Variable |

## How yield is generated

The strategy places limit lend orders in the USDFC fixed-rate markets according to fixed rules — the same rule framework as the [JPYC Lending Strategy](jpyc-lending-strategy.md#how-yield-is-generated), with its own parameter values:

* **Allocation:** deposits are split across the **two nearest eligible maturities** at a fixed **40% / 60%** ratio (nearest / next), set immutably at deployment.
* **Eligibility:** a maturity is excluded automatically when it is within the **maturity exclusion period (default: 7 days)** of expiry, or its order book is in Itayose / pre-order state, or the market is closed. When the nearest maturity enters the exclusion window, allocation shifts to the next eligible pair automatically.
* **Order placement:** **two limit lend orders per eligible maturity**, with the maturity's funds split **60% / 40%** between them. The first order is priced just below the current best lend price (or at the market mid where more favorable); additional orders are placed at **0.5% interest-rate increments** above the first (i.e. at slightly lower prices). All orders are subject to a **minimum APR floor of 3%**.
* **Rebalancing:** orders are re-placed only when recalculated target rates deviate from resting orders by more than **25 bps**, or when idle funds are at least **1 USDFC**. These conditions are publicly computable on-chain.
* **Capacity:** the vault has a deposit limit (currently **50,000 USDFC**).

*Example:* with 10,000 USDFC under management, 4,000 USDFC targets the nearest eligible maturity (placed as orders of 2,400 and 1,600) and 6,000 USDFC targets the next (3,600 and 2,400).

Interest earned on filled positions increases the Vault's total assets, which increases the value of Vault shares. Returns are **variable** and depend on market conditions.

## User experience

From the user's perspective:

* USDFC is deposited into the Vault
* Vault shares are received
* Yield accrues automatically over time
* Withdrawals are performed by redeeming shares

Users do not need to select lending terms, manage maturities, or rebalance positions.

## Liquidity and withdrawals — please read

Withdrawals are served in the same fixed order as the JPYC strategy — idle funds, then cancellation of the strategy's resting orders from the farthest maturity, then unwinding of positions from the nearest maturity against the live order book.

**Material limitation:** the final step depends on order-book liquidity. If the book cannot absorb the unwind, **the withdrawal transaction reverts** rather than executing at a distorted price. Funds remain in the vault; the withdrawal can be retried later or in smaller size. Withdrawal availability is therefore **not guaranteed at all times** and depends on market liquidity at the moment of withdrawal.

## Fees

* **Performance fee: 5% (500 bps) of realized profits**, accrued at report time to the on-chain designated fee recipient.
* The strategy charges **no fees on deposits or withdrawals**.
* Order execution in the underlying fixed-rate market incurs the protocol's standard order fee, as for any market participant; this cost is reflected in strategy returns.

Current fee parameters are readable directly from the strategy contract.

## Automated execution and governance

Execution involves **no per-trade discretionary decisions**. Strategy parameters are either fixed at deployment (maturity split, order count, minimum APR, maintenance threshold) or adjustable only through disclosed governance functions restricted to the **management** role (deposit limit; maturity exclusion period); every parameter change is an on-chain transaction, publicly visible and permanently auditable. A separate **keeper** role may call the maintenance functions (`tend` / `report`) only. The current management, keeper, and fee-recipient addresses are readable directly from the strategy contract ([Contracts and Security](../../contracts-and-security.md)), which is the authoritative source. The strategy contract's logic is **not upgradeable**, and share accounting is delegated to Yearn v3's audited `TokenizedStrategy` implementation. The framework is the same as the [JPYC Lending Strategy](jpyc-lending-strategy.md#automated-execution-and-governance).

The strategy cannot lend outside the Secured Finance USDFC markets, and cannot access depositor funds for any purpose other than the lending flows described here.

## Risk considerations

The USDFC Lending Strategy involves several types of risk, including but not limited to:

* **Liquidity / withdrawal risk** — withdrawals may fail temporarily when order-book liquidity is insufficient (see above)
* **Rate risk** — fixed-rate position values fluctuate with market rates until maturity; early unwinds execute at prevailing market prices
* **Roll risk** — auto-roll pricing depends on next-maturity order-book conditions at rotation
* **Smart contract risk** — vault, strategy, and protocol contracts may contain defects notwithstanding audits
* **Stablecoin risk** — USDFC collateral, peg, and issuance risk; see the [USDFC documentation](../../../usdfc-stablecoin/overview.md)

Users should understand that principal is not guaranteed, returns may fluctuate, and losses are possible under adverse conditions.

See also the protocol-wide [Risk Disclaimer](../../../resources/legal/risk-disclaimer.md).

## Related

* [JPYC Lending Strategy](jpyc-lending-strategy.md) — the same framework on Ethereum, with full rule detail
* [Strategy Framework and Allocation Model](../strategy-framework-and-allocation-model.md) — how strategies plug into vaults
* [Fixed-Rate Lending](../../../fixed-rate-lending/overview.md) — the markets this strategy lends into
