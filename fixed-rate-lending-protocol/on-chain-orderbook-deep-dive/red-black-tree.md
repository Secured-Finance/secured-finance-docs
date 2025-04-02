---
description: 'Reducing Gas Costs: A Computational Advantage'
---

# 🎋 Red Black Tree

A Red Black Tree is a balanced binary search tree that enables various operations such as data insertion, deletion, and search to be executed with a computational complexity of O(log n). In the context of Secured Finance, each node of this tree represents the Price in the order book, and it is linked to the corresponding Open Orders using a LinkedList, allowing efficient data management.

By utilizing the Red Black Tree, the gas cost associated with open order creation and deletion is significantly reduced to O(log n), resulting in substantial gas cost reductions. Moreover, for data updates, it is only necessary to update the target data and its adjacent data, eliminating the need to update the entire dataset and consequently avoiding gas costs proportional to the total data volume.

Furthermore, Secured Finance extends the functionality of the Red Black Tree by introducing a process to **Unlink** specified nodes. This **Unlink** operation effectively detaches all the data associated with the subtree rooted at the specified node. As a result, by simply **Unlink**ing certain nodes in the tree, all the data related to matched orders in the market can be removed from the order book.

Within a single order book, there are two separate Red Black Trees for managing Borrowing Orders and Lending Orders separately.



For more details on the process of unlinking nodes in the tree, please refer to the following documentation. (TBD)

