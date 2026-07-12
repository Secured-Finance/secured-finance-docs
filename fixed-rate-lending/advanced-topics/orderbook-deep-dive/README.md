---
description: Why a full on-chain order book is hard — and the three techniques that make ours economical
---

# Orderbook Deep Dive

A full on-chain order book is widely considered impractical: every open order is state, and Solidity storage writes are expensive. Three operations in particular scale badly with data volume — creating open orders, executing market orders against many resting orders, and rolling every position at maturity. Naively implemented, these can approach the block gas limit.

**Secured Finance runs a full on-chain order book anyway**, using three complementary techniques:

| Technique | What it solves |
| --- | --- |
| [**Red-Black Tree**](red-black-tree.md) | O(log n) insertion, deletion, and best-price lookup for orders, with a custom *unlink* operation for bulk removal of matched orders |
| [**Lazy Evaluation**](lazy-evaluation.md) | Defers state updates until a user actually acts — filled orders and matured positions are recomputed on read, not rewritten on every event |
| [**Genesis Value & Compound Factor**](genesis-value-and-compound-factor.md) | Rolls *every* position at maturity by updating a single factor, instead of touching each position individually |

Supporting structure: [**Orderbook Rotation**](orderbook-rotation.md) caps each currency at 9 order books (8 active + 1 pre-open), recycling matured markets so the data subject to lazy evaluation stays bounded.

{% hint style="info" %}
**Why bother?** Liquidity pools are simpler, but pool rates lack the transparency, composability, and term structure of an order book. Fixed income needs real price discovery at each maturity — that's what this architecture buys.
{% endhint %}
