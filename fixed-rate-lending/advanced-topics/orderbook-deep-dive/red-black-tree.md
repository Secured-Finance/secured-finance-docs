---
description: O(log n) order management with bulk unlinking
---

# 🎋 Red-Black Tree

Each order book stores its resting orders in **Red-Black Trees** — self-balancing binary search trees where insertion, deletion, and search are all **O(log n)**. Every node is a **price level**; orders at the same price hang off the node in a **linked list**, preserving first-come-first-served priority within the level.

Each order book maintains **two trees**: one for lend orders, one for borrow orders.

## Why it saves gas

* Inserting or removing an order touches only the O(log n) path to its node — never the whole book.
* Finding the best price is a walk to the tree's edge, also O(log n).
* Updates affect the target node and its neighbors only; total data volume doesn't multiply the cost.

For a book with 100 price levels, operations touch \~7 nodes instead of scanning 100 — an order-of-magnitude gas reduction versus array-based structures.

## The unlink extension

Secured Finance extends the standard structure with an **unlink** operation: when orders are matched, the affected nodes (or entire subtrees) are _marked detached_ in O(1) rather than physically deleted and rebalanced. Traversals skip unlinked entries; physical cleanup happens later, batched into transactions that already pay for storage writes (see [Lazy Evaluation](lazy-evaluation.md)).

This matters most when many orders match at once — a large market order sweeping several levels, or an [Itayose](../itayose.md) auction filling an entire overlap range — where per-order deletion would multiply gas costs.

## Life of an order in the tree

1. Alice places a limit lend order at price 95.24 → if a node for 95.24 exists, her order appends to its list; otherwise a new node is inserted (O(log n)) and the tree rebalances if needed.
2. Bob's market order matches Alice's → her order is **unlinked** (O(1)); the tree structure is untouched.
3. A later user action triggers cleanup → empty nodes are physically removed in a batch.

## Related

* [Lazy Evaluation](lazy-evaluation.md) — the deferred-cleanup principle
* [Order Book & Order Types](../../core-concepts/order-book.md) — the user-facing view
