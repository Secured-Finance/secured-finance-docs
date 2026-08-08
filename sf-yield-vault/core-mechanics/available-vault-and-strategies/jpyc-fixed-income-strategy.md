# 💹 JPYC Lending Strategy

#### Overview

The **JPYC Lending Strategy** is the first strategy deployed within the [**JPYC Vault**](https://vaults.secured.finance/1/0x7a6E3635694952dC00F6bA4d4AD1a7B892028789) under the Secured Finance framework.

This strategy is designed to generate yield by deploying **JPYC** into the Secured Finance fixed-rate lending markets, allowing Vault participants to earn variable returns without actively managing positions.

The strategy is **fully rule-based**: every rule described on this page is encoded in the deployed strategy contract, which can be inspected on-chain directly from the Vault page.

***

#### Purpose of the Strategy

The primary objectives of the JPYC Lending Strategy are:

* To provide a simple, automated way to earn yield on JPYC
* To abstract away lending market operations from users
* To integrate JPYC into the broader Secured Finance fixed-income ecosystem

Users interact with the Vault, not the strategy directly.

***

#### How Yield Is Generated

The strategy places limit lend orders in the JPYC fixed-rate markets according to fixed rules:

* **Allocation:** deposits are split across the **two nearest eligible maturities** at a fixed **40% / 60%** ratio (nearest / next), set immutably at deployment.
* **Eligibility:** a maturity is excluded automatically when it is within the **maturity exclusion period (default: 7 days)** of expiry, or its order book is in Itayose / pre-order state, or the market is closed. When the nearest maturity enters the exclusion window, allocation shifts to the next eligible pair automatically.
* **Order placement:** one limit lend order per eligible maturity, priced just below the current best lend price (or at the market mid where more favorable), subject to a **minimum APR floor of 1%**.
* **Rebalancing:** orders are re-placed only when recalculated target rates deviate from resting orders by more than **25 bps**, or when idle funds exceed **100,000 JPYC**. These conditions are publicly computable on-chain.
* **Capacity:** the vault has a deposit limit (currently **50,000,000 JPYC**).

Interest earned on filled positions increases the Vault's total assets, which increases the value of Vault shares. Returns are **variable** and depend on market conditions.

***

#### User Experience

From the user's perspective:

* JPYC is deposited into the Vault
* Vault shares are received
* Yield accrues automatically over time
* Withdrawals are performed by redeeming shares

Users do not need to select lending terms, manage maturities, or rebalance positions.

***

#### Relationship to Fixed-Rate Lending

The JPYC Lending Strategy differs from Secured Finance's Fixed-Rate Lending product in several key ways:

* **JPYC Lending Strategy**
  * Variable yield
  * No fixed maturity
  * Fully automated allocation
* **Fixed-Rate Lending**
  * Fixed interest rate
  * Defined maturity
  * Direct position management

Both products coexist within the ecosystem and serve different user preferences.

***

#### Liquidity and Withdrawals — please read

Withdrawals are served in a fixed order:

1. **Idle funds** held by the vault and strategy;
2. **Cancellation of the strategy's own resting orders**, starting from the farthest maturity (preserving near-term positions);
3. **Unwinding of positions**, starting from the nearest maturity, executed against the live order book.

**Material limitation:** step 3 depends on order-book liquidity. If the book cannot absorb the unwind, **the withdrawal transaction reverts** ("Not enough funds freed") rather than executing at a distorted price or realizing an artificial loss. Funds remain in the vault; the withdrawal can be retried later or in smaller size. Withdrawal availability is therefore **not guaranteed at all times** and depends on market liquidity at the moment of withdrawal.

Positions held to maturity are auto-rolled into the next maturity by the protocol's rotation mechanism; roll pricing is determined by the next maturity's order book at rotation time, with no strategy discretion.

***

#### Fees

* **Performance fee: 5% (500 bps) of realized profits**, accrued at report time to the on-chain designated fee recipient.
* The strategy charges **no fees on deposits or withdrawals**.
* Order execution in the underlying fixed-rate market incurs the protocol's standard order fee, as for any market participant; this cost is reflected in strategy returns.

Current fee parameters are readable directly from the strategy contract.

***

#### Automated Execution and Governance

* Execution involves **no per-trade discretionary decisions**: no person selects individual trades, counterparties, timing, or prices.
* Strategy parameters are either **fixed at deployment** (maturity split, order count, minimum APR, maintenance threshold) or adjustable **only** through disclosed governance functions restricted to the management role (**deposit limit; maturity exclusion period**). Every parameter change is an on-chain transaction, publicly visible and permanently auditable.
* The **management** role governs the adjustable parameters above; a separate **keeper** role may call the maintenance functions (`tend` / `report`) only. The current management, keeper, and fee-recipient addresses are readable directly from the strategy contract, which is the authoritative source.
* The strategy contract's logic is **not upgradeable**. Share accounting is delegated to Yearn v3's audited `TokenizedStrategy` implementation.

The strategy cannot lend outside the Secured Finance JPYC markets defined above, and cannot access depositor funds for any purpose other than the lending flows described here.

***

#### Risk Considerations

The JPYC Lending Strategy involves several types of risk, including but not limited to:

* **Liquidity / withdrawal risk** — withdrawals may fail temporarily when order-book liquidity is insufficient (see above)
* **Rate risk** — fixed-rate position values fluctuate with market rates until maturity; early unwinds execute at prevailing market prices
* **Roll risk** — auto-roll pricing depends on next-maturity order-book conditions at rotation
* **Smart contract risk** — vault, strategy, and protocol contracts may contain defects notwithstanding audits
* **Stablecoin risk** — JPYC issuer and peg risk

Users should understand that principal is not guaranteed, returns may fluctuate, and losses are possible under adverse conditions.

***

#### Future Evolution

The strategy may be complemented or replaced by additional strategies over time. Any strategy deployment or parameter change is an on-chain transaction and will be reflected in updated documentation.
