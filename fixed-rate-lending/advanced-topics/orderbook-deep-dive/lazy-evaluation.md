---
description: Compute on read, not on write — the protocol's core gas strategy
---

# Lazy Evaluation

**Lazy evaluation** defers computation and storage updates until they're actually needed. Instead of rewriting state every time an order fills or a market matures, the protocol records the minimal facts and reconstructs current values **on read**. Storage writes are the most expensive operation on the EVM; reads and computation are cheap — lazy evaluation trades the former for the latter.

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption><p>How an order's value is converted from order amount to future value, then to genesis value</p></figcaption></figure>

## The three states of user funds

| State | Representation | Lazy behavior |
| --- | --- | --- |
| **Open order** | Entry in the order book tree | Fill status checked via [unlink markers](red-black-tree.md) on read — no storage update when matched |
| **Active position** | Future Value (FV) | Valued on read; when its market matures, it's *treated as* rolled without any write |
| **Auto-rolled position** | Genesis Value (GV) | Value derived from the global [Compound Factor](genesis-value-and-compound-factor.md) — one update rolls everyone |

When you query your balance, the contract computes the true current amount in real time from these representations — always up to date, never stale, no batch jobs.

## CleanUp: when writes actually happen

Deferred state is settled by an implicit **CleanUp** during operations that already pay for storage — placing an order, withdrawing collateral, minting/burning ZC tokens. At that point matched orders are physically removed and matured positions are formally converted to GV. Users never trigger cleanup explicitly.

## Why it's essential, not optional

* **Auto-Roll** without lazy evaluation would mean updating *every position in a market* at maturity — thousands of writes in one block, breaching gas limits. With GV accounting it's a single factor update.
* **Market orders** sweeping many resting orders would pay per-order deletion costs; unlinking makes matching O(1) per matched order.
* **[Orderbook Rotation](orderbook-rotation.md)** caps the books per currency at 9, keeping the data subject to lazy evaluation bounded forever.

## Does deferral risk inconsistency?

No. The derivations are deterministic: given the same on-chain facts, a read always produces the same value, whether cleanup has run or not. Deferral changes *when* storage is written, never *what* the position is worth.

## Related

* [Genesis Value & Compound Factor](genesis-value-and-compound-factor.md) — the accounting that makes rolls O(1)
* [Red-Black Tree](red-black-tree.md) — unlinking in the order book
