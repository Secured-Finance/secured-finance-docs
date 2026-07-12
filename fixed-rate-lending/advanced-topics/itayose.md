---
description: The opening auction that sets a fair price for every new market
---

# Itayose: Fair Price Discovery

**Itayose** (板寄せ — the call-auction method used by Japanese exchanges) determines the opening price whenever a new order book starts trading. Instead of letting the first trade set an arbitrary price, all pre-open orders are matched simultaneously at a single fair price.

## The three phases

### Before opening (pre-open period)

* Starting **7 days** before a new order book opens, users may place **limit orders only**, and only on **one side** (you can't quote both sides — a manipulation guard).
* The app displays the **estimated opening APR** based on the evolving pre-open book.
* **1 hour** before opening, the book freezes — no placing, amending, or canceling.

### During Itayose

The smart contract consolidates all overlapping bids and offers and computes the opening price to **maximize executed volume**, considering total lend amount, total borrow amount, and the imbalance between them. With no imbalance, the mid-price is taken; with an imbalance, the price moves toward the heavier side. If no orders overlap, the market simply opens without an opening price.

{% hint style="info" %}
**Fees are waived for all orders filled during Itayose** — an incentive to participate in price discovery.
{% endhint %}

### After opening

Orders executed by Itayose all fill at the single opening price. Unfilled orders remain on the book as normal limit orders when continuous trading begins.

## Worked examples

**Balanced book:** lend orders total 100,000 USDC and borrow orders total 100,000 USDC in the overlapping range 98.10–98.40 → the opening price is the mid, **98.25**, and everything fills.

**Imbalanced book (more lenders):** 180,000 USDC of lend orders vs 120,000 USDC of borrow orders overlap in 97.60–97.90 → the price settles toward the lend side at **97.70**; all 120,000 of borrows fill, lend orders fill 120,000 by time priority, and the remaining 60,000 rest on the book at open.

**No overlap:** highest borrow price 95.80 < lowest lend price 96.00 → no matching; the market opens with all pre-orders resting.

## Why it matters

* **Fair access** — everyone who participates gets the same opening price
* **Liquidity from block one** — new markets open with a populated book, not a void
* **Manipulation resistance** — single-side quoting, the freeze window, and volume-maximizing pricing make the open hard to game

## Related

* [Market Listing & Delisting](market-listing-and-delisting.md) — when Itayose runs
* [Orderbook Rotation](orderbook-deep-dive/orderbook-rotation.md) — the quarterly cycle it belongs to
* [Fees](../core-concepts/fees.md) — the Itayose fee waiver
