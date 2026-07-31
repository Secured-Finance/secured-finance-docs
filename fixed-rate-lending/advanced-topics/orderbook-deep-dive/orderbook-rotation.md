---
description: The quarterly recycling cycle that keeps gas costs bounded
---

# Orderbook Rotation

Each currency runs exactly **9 order book contracts: 8 active + 1 inactive**. Rather than deploying new contracts each quarter, matured order books are **recycled** — a design that both avoids deployment costs and caps the data volume that [lazy evaluation](lazy-evaluation.md) must handle.

## The cycle

1. The **inactive** order book opens a **7-day pre-order period** for the next new maturity (2 years out), ending 1 hour before the nearest active book matures.
2. At maturity: the [Itayose](../itayose.md) auction runs and the new book **activates**; the matured book's positions [auto-roll](../../core-concepts/fixed-maturity-and-auto-roll.md); the matured book itself moves to the end of the queue and becomes the new **inactive** book.
3. The cycle repeats every quarter.

**Example (ETH):** active books MAR26…DEC27, inactive book preparing MAR28. When MAR26 matures, MAR28 opens via Itayose, MAR26's positions roll into JUN26 (nearest 3-month), and the MAR26 contract is recycled to prepare JUN28.

<!-- figure: market-life-cycle (redraw of former diagram) -->

## Why exactly 9?

* **Gas bound** — order placement and matching never consider more than 8 active books' data; lazy evaluation has a fixed-size working set.
* **Liquidity concentration** — 8 quarterly points cover 2 years without fragmenting volume across dozens of dates.
* **No deployment churn** — recycling reuses contracts, so the protocol's address surface stays stable.

## Related

* [Fixed Maturity & Auto-Roll](../../core-concepts/fixed-maturity-and-auto-roll.md) — the user-facing view of the same cycle
* [Itayose](../itayose.md) — how the new book's opening price is set
