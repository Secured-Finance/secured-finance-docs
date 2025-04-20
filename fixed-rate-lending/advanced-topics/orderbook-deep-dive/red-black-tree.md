---
description: Understanding how Red-Black Trees optimize orderbook operations and reduce gas costs in the Fixed-Rate Lending Protocol
icon: 🎋
---

# 🎋 Red Black Tree

## Overview

A Red Black Tree is a balanced binary search tree that enables various operations such as data insertion, deletion, and search to be executed with a computational complexity of O(log n). In the context of Secured Finance, each node of this tree represents the Price in the order book, and it is linked to the corresponding Open Orders using a LinkedList, allowing efficient data management and significant gas cost reductions.

## What You'll Learn

- How Red-Black Trees are implemented in the Fixed-Rate Lending Protocol
- Why this data structure is crucial for gas cost optimization
- How the Unlink operation enhances orderbook efficiency
- How Borrowing and Lending Orders are managed separately
- The computational advantages of using Red-Black Trees for orderbooks

## How It Works

Red-Black Trees provide an efficient way to organize and manage orderbook data, significantly reducing gas costs and improving overall protocol performance.

### Computational Efficiency

By utilizing the Red Black Tree, the gas cost associated with open order creation and deletion is significantly reduced to O(log n), resulting in substantial gas cost reductions. Moreover, for data updates, it is only necessary to update the target data and its adjacent data, eliminating the need to update the entire dataset and consequently avoiding gas costs proportional to the total data volume.

### Enhanced Unlinking Process

Secured Finance extends the functionality of the Red Black Tree by introducing a process to **Unlink** specified nodes. This **Unlink** operation effectively detaches all the data associated with the subtree rooted at the specified node. As a result, by simply **Unlink**ing certain nodes in the tree, all the data related to matched orders in the market can be removed from the order book.

### Separate Trees for Order Types

Within a single order book, there are two separate Red Black Trees for managing Borrowing Orders and Lending Orders separately. This separation allows for more efficient order matching and management, as each tree can be optimized for its specific order type.

### Order Management

Each price level in the orderbook is represented by a node in the Red-Black Tree. Orders at the same price level are linked together using a LinkedList structure, allowing for efficient insertion and removal of orders at a specific price point. When orders are matched, the corresponding nodes can be efficiently unlinked from the tree without affecting the overall structure.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Computational Complexity | Time complexity for insertion, deletion, and search operations | O(log n) |
| Tree Structure | Type of balanced binary search tree used | Red-Black Tree |
| Node Representation | What each node in the tree represents | Price level in orderbook |
| Order Storage | How orders at the same price are stored | LinkedList |
| Number of Trees per Orderbook | Separate trees for different order types | 2 (Borrowing and Lending) |
| Unlinking Operation | Special operation for efficient order removal | Custom implementation |

## Related Resources

- [Orderbook Deep Dive](README.md)
- [Lazy Evaluation](lazy-evaluation.md)
- [Order Book System](../../../core-mechanics/order-book-system/README.md)
- [Order Types](../../../core-mechanics/order-book-system/order-type.md)
- [Order Life Cycle](../../../core-mechanics/order-book-system/order-life-cycle/case-study-order-status-and-transition.md)

