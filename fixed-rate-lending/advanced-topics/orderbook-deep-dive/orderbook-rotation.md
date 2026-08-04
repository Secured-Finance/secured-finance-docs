---
description: The quarterly recycling cycle that keeps gas costs bounded
---

# Orderbook Rotation

At the full standard configuration, each currency runs **9 order books (8 active + 1 inactive) inside a single lending market contract**; a market with less liquidity may keep fewer maturities open. Rather than creating new order books each quarter, matured ones are **recycled** — a design that both avoids deployment costs and caps the data volume that [lazy evaluation](lazy-evaluation.md) must handle.

## The cycle

1. The **inactive** order book opens a **7-day pre-order period** for the next new maturity (2 years out), ending 1 hour before the nearest active book matures.
2. At maturity: the [Itayose](../itayose.md) auction runs and the new book **activates**; the matured book's positions [auto-roll](../../core-concepts/fixed-maturity-and-auto-roll.md); the matured book itself moves to the end of the queue and becomes the new **inactive** book.
3. The cycle repeats every quarter.

**Example (ETH):** active books MAR2026…DEC2027, inactive book preparing MAR2028. When MAR2026 matures, MAR2028 opens via Itayose, MAR2026's positions roll into JUN2026 (nearest 3-month), and the MAR2026 order book is recycled to prepare JUN2028.

<!-- figure: market-life-cycle (redraw of former diagram) -->
<figure><img src="../../../.gitbook/assets/Market Kife Cycle (1).png" alt=""><figcaption><p>Market Life Cycle</p></figcaption></figure>

## Why exactly 9?

* **Gas bound** — order placement and matching never consider more than 8 active books' data; lazy evaluation has a fixed-size working set.
* **Liquidity concentration** — 8 quarterly points cover 2 years without fragmenting volume across dozens of dates.
* **No deployment churn** — recycling reuses order books within the same contract, so the protocol's address surface stays stable.

## Related

* [Fixed Maturity & Auto-Roll](../../core-concepts/fixed-maturity-and-auto-roll.md) — the user-facing view of the same cycle
* [Itayose](../itayose.md) — how the new book's opening price is set
