---
description: Available Strategies
---

# 📏 Available Vault and Strategies

#### Overview

This section introduces the **strategies currently available within Vaults**.

A strategy defines how assets deposited into a Vault are deployed to generate yield. Vaults may support one or multiple strategies, and strategies may evolve over time as the protocol expands.

This page serves as a **navigation hub** for strategy-specific documentation.

***

#### How to Read This Section

For each strategy, you will find a dedicated page that explains:

* The purpose of the strategy
* How yield is generated (at a high level)
* Key characteristics and constraints
* Risk considerations relevant to users

Strategy pages are written to complement the **Core Mechanics** section and focus on strategy-specific behavior, rather than Vault infrastructure.

***

#### Currently Available Strategies

* [**JPYC Lending Strategy**](jpyc-fixed-income-strategy.md)\
  A lending-based strategy that deploys JPYC to generate variable yield.
* [**USDFC Lending Strategy**](usdfc-lending-strategy.md)\
  A lending-based strategy that deploys USDFC to generate variable yield.

Additional strategies may be introduced in the future and will be listed here as they become available.

***

#### Strategy Availability and Changes

Strategies are not static.

Over time, strategies may be:

* Added
* Updated
* Paused
* Deprecated

Such changes are handled through governance or operational processes.

Vaults are designed so that strategy changes do not require users to change how they interact with the Vault.
