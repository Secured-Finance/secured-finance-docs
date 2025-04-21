---
description: Understanding how Red-Black Trees optimize orderbook operations and reduce gas costs in the Fixed-Rate Lending Protocol
icon: 🎋
---

# 🎋 Red Black Tree

## Overview

A Red Black Tree is a balanced binary search tree that enables various operations such as data insertion, deletion, and search to be executed with a computational complexity of O(log n). In the context of Secured Finance, each node of this tree represents the Price in the order book, and it is linked to the corresponding Open Orders using a LinkedList, allowing efficient data management and significant gas cost reductions.

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

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption><p>Red-Black Tree Structure in Orderbook</p></figcaption></figure>

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Computational Complexity | Time complexity for insertion, deletion, and search operations | O(log n) |
| Tree Structure | Type of balanced binary search tree used | Red-Black Tree |
| Node Representation | What each node in the tree represents | Price level in orderbook |
| Order Storage | How orders at the same price are stored | LinkedList |
| Number of Trees per Orderbook | Separate trees for different order types | 2 (Borrowing and Lending) |
| Unlinking Operation | Special operation for efficient order removal | Custom implementation |
| Rebalancing Threshold | When tree rebalancing occurs | After insertion/deletion |
| Maximum Tree Depth | Worst-case depth of the tree with n nodes | 2×log₂(n+1) |
| Color Property | Colors used in the Red-Black Tree | Red and Black |
| Tree Properties | Rules that maintain tree balance | 5 standard Red-Black Tree properties |

## Examples

### Example 1: Order Insertion Process

Let's walk through how a new order is inserted into the orderbook:

1. Alice places a limit order to lend 1,000 USDC at 5% APR in the JUN2025 market
2. The protocol converts the 5% APR to a price value (e.g., 0.95238)
3. The system checks if a node for price 0.95238 already exists in the Lending Orders Red-Black Tree:
   - If it exists: Alice's order is added to the LinkedList of orders at that price point
   - If it doesn't exist: A new node is created with price 0.95238, and Alice's order becomes the first in the LinkedList
4. The Red-Black Tree is rebalanced if necessary to maintain its properties
5. The entire operation has O(log n) time complexity, where n is the number of distinct price levels
6. Gas cost is significantly lower than if a linear data structure were used

### Example 2: Order Matching and Unlinking

When orders are matched in the orderbook:

1. Bob places a market order to borrow 2,000 USDC in the JUN2025 market
2. The system traverses the Lending Orders Red-Black Tree to find the best available rates
3. It finds multiple lending orders, including Alice's order at 5% APR
4. After matching, Alice's order is fully filled
5. Instead of immediately removing Alice's order from the LinkedList and potentially the tree node:
   - The system marks Alice's order as "unlinked"
   - The order remains in the data structure but is ignored during traversal
6. During a later CleanUp process:
   - If Alice's order was the only one at that price point, the entire node is removed
   - If other orders exist at that price, only Alice's order is removed from the LinkedList
7. This deferred cleanup (lazy evaluation) further reduces gas costs

### Example 3: Gas Cost Comparison

Consider the gas cost implications of different data structures for an orderbook with 100 price levels and 1,000 total orders:

1. **Array-based implementation**:
   - Inserting a new order: O(n) = O(100) operations
   - Finding the best price: O(n) = O(100) operations
   - Removing a matched order: O(n) = O(100) operations
   - Total gas cost for 100 transactions: Approximately 3,000,000 gas

2. **Red-Black Tree implementation**:
   - Inserting a new order: O(log n) = O(log 100) ≈ O(7) operations
   - Finding the best price: O(log n) = O(log 100) ≈ O(7) operations
   - Removing a matched order: O(log n) = O(log 100) ≈ O(7) operations
   - Total gas cost for 100 transactions: Approximately 500,000 gas

3. **Red-Black Tree with Unlinking and Lazy Evaluation**:
   - Inserting a new order: O(log n) = O(log 100) ≈ O(7) operations
   - Finding the best price: O(log n) = O(log 100) ≈ O(7) operations
   - Marking an order as unlinked: O(1) operation
   - Batch cleanup of multiple unlinked orders: Amortized O(1) per order
   - Total gas cost for 100 transactions: Approximately 300,000 gas

The Red-Black Tree with unlinking provides an 85-90% reduction in gas costs compared to naive implementations.

## FAQ

### Why use Red-Black Trees instead of other data structures?

Red-Black Trees offer several advantages for orderbook implementation:

1. **Balanced Structure**: Red-Black Trees are self-balancing, ensuring O(log n) operations even in worst-case scenarios
2. **Ordered Traversal**: The tree structure allows for efficient in-order traversal to find the best prices
3. **Memory Efficiency**: The tree structure is more memory-efficient than maintaining sorted arrays
4. **Insertion/Deletion Performance**: Both operations are O(log n), making them efficient for dynamic orderbooks
5. **Proven Technology**: Red-Black Trees are a well-established data structure with known properties and guarantees

While other balanced binary search trees like AVL trees could also work, Red-Black Trees offer a good balance between performance and implementation complexity.

### How does the Unlink operation differ from standard deletion?

The Unlink operation is a specialized optimization that differs from standard tree deletion:

1. **Standard Deletion**: Completely removes a node from the tree, requiring tree rebalancing
2. **Unlinking**: Marks a node or order as "unlinked" without removing it from the data structure
3. **Deferred Cleanup**: Actual removal happens later during batch operations
4. **Gas Efficiency**: Unlinking is an O(1) operation, while deletion is O(log n)
5. **Batch Processing**: Multiple unlinked nodes can be cleaned up in a single operation

This approach is particularly valuable in blockchain contexts where minimizing gas costs is critical.

### How do Red-Black Trees handle multiple orders at the same price?

To handle multiple orders at the same price point:

1. **Node Structure**: Each node in the Red-Black Tree represents a unique price point
2. **LinkedList Integration**: All orders at the same price are stored in a LinkedList attached to the node
3. **Order Priority**: Within a price point, orders are typically prioritized by time (FIFO)
4. **Partial Fills**: When an order is partially filled, it remains in the LinkedList with an updated amount
5. **Complete Fills**: When an order is completely filled, it's marked as unlinked in the LinkedList

This hybrid data structure combines the efficiency of Red-Black Trees for price discovery with the simplicity of LinkedLists for order queuing.

### What happens when a large number of orders are matched at once?

When many orders are matched simultaneously (e.g., during Itayose price discovery):

1. **Batch Processing**: The system processes multiple matches in a single transaction
2. **Efficient Unlinking**: Orders are marked as unlinked rather than immediately removed
3. **Subtree Unlinking**: In some cases, entire subtrees can be unlinked at once
4. **Deferred Cleanup**: The actual removal of unlinked orders happens during less time-sensitive operations
5. **Gas Optimization**: This approach significantly reduces the gas cost of large-scale order matching

This is particularly important during events like auto-rolling or new market openings when many orders may be matched simultaneously.

### How are the Red-Black Trees maintained across multiple orderbooks?

The protocol maintains separate Red-Black Trees for each orderbook and order type:

1. **Per-Market Trees**: Each market (maturity date) has its own set of Red-Black Trees
2. **Order Type Separation**: Within each market, separate trees exist for Borrowing and Lending orders
3. **Recycling**: When markets mature, the tree structures are recycled for new markets
4. **Consistent Interface**: Despite having multiple trees, the protocol provides a unified interface for interacting with them
5. **Parallel Processing**: The separation allows for more efficient processing of different order types

This modular approach helps maintain performance even as the number of markets and orders grows.

## Related Resources

- [Orderbook Deep Dive](README.md)
- [Lazy Evaluation](lazy-evaluation.md)
- [Order Book System](../../../core-mechanics/order-book-system/README.md)
- [Order Types](../../../core-mechanics/order-book-system/order-type.md)
- [Order Life Cycle](../../../core-mechanics/order-book-system/order-life-cycle/case-study-order-status-and-transition.md)

