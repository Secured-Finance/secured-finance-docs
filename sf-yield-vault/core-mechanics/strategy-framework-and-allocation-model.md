# 💿 Strategy Framework and Allocation Model

#### Purpose of This Page

This page explains how strategies integrate with Vaults and how capital is allocated, managed, and withdrawn.

***

#### What Is a Strategy?

A **Strategy** is a contract responsible for generating yield using Vault assets.

Each strategy:

* Accepts assets from the Vault
* Deploys them according to its own logic
* Reports balances and performance back to the Vault

Strategies are designed to be **independent and reusable**. A single strategy may be connected to multiple Vaults, depending on configuration.

***

#### Strategy Responsibilities

From the Vault’s perspective, a strategy must be able to:

* Receive assets
* Return assets on request (subject to liquidity constraints)
* Accurately report its current balance
* Reflect gains or losses over time

How the strategy achieves this is intentionally left abstract at the Vault level.

***

#### Allocation Model

Vaults allocate capital to strategies based on configuration parameters.

These may include:

* Maximum allocation limits
* Strategy capacity
* Liquidity characteristics
* Risk considerations

A Vault may:

* Use a single strategy
* Distribute capital across multiple strategies
* Adjust allocations over time

The allocation logic can evolve without changing the Vault interface.

***

#### Strategy Lifecycle

Strategies typically follow a defined lifecycle:

1. Deployment
2. Registration with the system
3. Activation for allocation
4. Ongoing operation and reporting
5. Allocation reduction or pause
6. Removal, if necessary

This lifecycle allows strategies to be managed safely without forcing users to exit the Vault.

***

#### Handling Yield and Losses

Strategies may generate:

* Positive yield
* No yield
* Temporary or permanent losses

All outcomes are reflected at the Vault level through changes in total assets.

Vault Shares automatically adjust in value to reflect strategy performance, without requiring user action.

***

#### Risk Boundaries

It is important to clearly define what the Vault does and does not guarantee.

* Vaults do not guarantee principal
* Vaults do not guarantee yield
* Strategy risk is borne collectively by Vault participants

The modular design allows risk to be managed, but not eliminated.

***

#### Why This Framework Matters

This strategy framework enables:

* Incremental addition of new strategies
* Experimentation without disrupting users
* Clear separation between infrastructure and execution
* Long-term scalability of the Vault system
