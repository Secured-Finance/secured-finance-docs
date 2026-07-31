---
description: Your assets, collateral, positions, and history in one place
---

# Portfolio

The [**Portfolio**](https://app.secured.finance/portfolio/) tab is your account home: deposits, withdrawals, collateral health, positions, and full history.

<!-- screenshot: portfolio-overview -->

## Overview metrics

* **Net Asset Value** — total value of your deposits and positions on the platform
* **Active Contracts** — count of your open lending/borrowing positions
* **Lending PV / Borrowing PV** — present value of each side of your book

## Assets

* **Collateral balance** — deposited assets backing your borrows, and their utilization
* **Non-collateral assets** — deposited assets not eligible (or not used) as collateral
* **Deposit / Withdraw** buttons — move assets between your wallet and the protocol

## Risk panel (borrowers)

* **Collateral utilization** — how much of your capacity is in use
* **Liquidation risk indicator** — green → yellow → red as your LTV approaches the liquidation threshold ([current values](../../protocol-parameters.md))

When the indicator trends red: deposit more collateral or partially [unwind](../managing-positions.md) borrow positions. See [Liquidation](../../core-concepts/liquidation/README.md).

## Transactions

Four tabs cover your full activity: **Active Positions** (open positions, with Unwind actions), **Open Orders** (resting limit orders, cancellable), **Order History**, and **My Transactions**.

## Related

* [Managing Your Positions](../managing-positions.md) — unwind, add, reduce
* [Tokenization](../../core-concepts/tokenization.md) — withdraw a lending position as an ERC-20 ZC Token
