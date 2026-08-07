# 💹 JPYC Fixed-Income Strategy

#### Overview

The **JPYC Lending Strategy** is the first strategy deployed within the [**JPYC Vault**](https://vaults.secured.finance/1/0x7a6E3635694952dC00F6bA4d4AD1a7B892028789) under the Secured Finance framework.

This strategy is designed to generate yield by deploying **JPYC** into lending activities, allowing Vault participants to earn variable returns without actively managing positions.

The JPYC Lending Strategy operates within the shared Vault infrastructure described in previous sections.

***

#### Purpose of the Strategy

The primary objectives of the JPYC Lending Strategy are:

* To provide a simple, automated way to earn yield on JPYC
* To abstract away lending market operations from users
* To integrate JPYC into the broader Secured Finance fixed-income ecosystem

Users interact with the Vault, not the strategy directly.

***

#### How Yield Is Generated

At a high level, the strategy generates yield by:

* Allocating JPYC supplied by the Vault to lending mechanisms
* Earning interest from borrowers over time
* Returning accrued interest to the Vault

The resulting yield is reflected as an increase in the Vault’s total assets, which in turn increases the value of Vault shares.

Returns are **variable** and depend on market conditions.

***

#### User Experience

From the user’s perspective:

* JPYC is deposited into the Vault
* Vault shares are received
* Yield accrues automatically over time
* Withdrawals are performed by redeeming shares

Users do not need to select lending terms, manage maturities, or rebalance positions.

***

#### Relationship to Fixed-Rate Lending

The JPYC Lending Strategy differs from Secured Finance’s Fixed-Rate Lending product in several key ways:

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

#### Liquidity and Withdrawals

Withdrawals from the Vault depend on the liquidity available within the strategy.

While the strategy is designed to support regular withdrawals, certain market conditions may affect withdrawal timing or amounts.

Details regarding liquidity behavior are covered in the **Risk Considerations** section.

***

#### Risk Considerations

The JPYC Lending Strategy involves several types of risk, including but not limited to:

* Smart contract risk
* Lending market risk
* Liquidity risk
* Counterparty or protocol dependency risk

Users should understand that:

* Principal is not guaranteed
* Returns may fluctuate
* Losses are possible under adverse conditions

***

#### Strategy Scope and Limitations

This strategy focuses specifically on:

* JPYC as the base asset
* Lending-based yield generation

It does not:

* Guarantee a minimum return
* Provide fixed-rate outcomes
* Eliminate all forms of risk

***

#### Future Evolution

The JPYC Lending Strategy represents the initial implementation within the Vault framework.

Over time, the strategy may:

* Be adjusted or optimized
* Be complemented by additional JPYC strategies
* Serve as a reference model for future lending strategies

Any material changes will be reflected in updated documentation.
