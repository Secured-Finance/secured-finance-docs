---
description: Understanding how Lazy Evaluation optimizes gas costs and improves efficiency in the Fixed-Rate Lending Protocol
icon: ⏯️
---

# ⏯️ Lazy Evaluation

## Overview

Secured Finance has introduced a revolutionary feature known as "lazy evaluation," which significantly streamlines the management of orders and the auto-roll process. This mechanism works by deferring the computation and update of orders and positions until absolutely necessary. As a result, it eliminates the need to manually roll over each position or update a multitude of open orders whenever an order is filled. This approach not only leads to substantial savings in gas costs but also boosts the overall efficiency of the protocol.

## How It Works

Lazy Evaluation defers computations until they are absolutely necessary, significantly reducing gas costs and improving protocol efficiency.

### States of Orders

Orders in the system can exist in three states, all of which utilize Lazy Evaluation:

1. **Open Order**: Remaining Orders which are not filled on our orderbook system.
2. **Active Position (FV)**: Once Orders are filled, they will be managed by Future Value (FV).
3. **Auto-rolled Position (GV)**: Positions that have reached their maturity date will be Auto-rolled without any action and managed by Genesis Value (GV).

**Lazy evaluation is utilized for all states above**. For Open Orders, the contract checks if the order has been unlinked on the red-black tree, indicating that the order has already been filled. As for Active Positions (FV), if the positions reach their maturity date, they are then treated as Auto-rolled Positions (GV) and returned as such. As for Auto-rolled Positions (GV), only borrowing positions will increase after each roll. (Please refer to the [Compound Factor](compound-factor.md) for more detail)

### State Updates

Lazy evaluation continues to be applied to these data as long as they exist. However, when a CleanUp process is executed, the state of the data changes, and they are no longer subject to lazy evaluation once it turned to GV. CleanUp processes are implicitly executed during certain operations taken by users such as order execution, collateral withdrawals, and so on.

{% hint style="info" %}
To optimize the gas costs of lazy evaluation, market contracts that have reached maturity are recycled, and new markets are opened. This ensures efficient utilization of gas costs for lazy evaluation. Please refer to the [Orderbook Life Cycle](orderbook-rotation.md)
{% endhint %}

### Smart Contract Storage and Real-Time Calculation

The above states are stored on the smart contract storage, ensuring data integrity and consistency. When a user calls the smart contract to retrieve their own amount, the system calculates the actual amount in real-time, providing up-to-date and accurate information.

### Importance in Supporting Key Functionalities

Lazy order evaluation is a critical component for supporting essential functionalities such as market orders and auto-roll. Without it, executing these operations would result in substantial gas costs, particularly in terms of storage. By adopting lazy evaluation, Secured Finance streamlines its platform and ensures a more cost-effective and user-friendly experience for all participants.

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption><p>Lazy Evaluation Process Flow</p></figcaption></figure>

## Examples

### Example 1: Lazy Evaluation for Open Orders

Let's consider how lazy evaluation works for open orders:

1. Alice places a limit order to lend 1,000 USDC at 5% APR in the JUN2025 market
2. Bob places a market order to borrow 500 USDC, which partially fills Alice's order
3. Without lazy evaluation, the system would need to:
   - Update Alice's order to show 500 USDC remaining
   - Create a new position record for the filled portion
   - Update multiple storage slots, costing significant gas
4. With lazy evaluation:
   - The system marks Alice's order as "unlinked" in the red-black tree
   - When Alice queries her position, the contract calculates in real-time:
     - Original order: 1,000 USDC
     - Filled amount: 500 USDC
     - Remaining: 500 USDC
   - No storage updates are needed until Alice takes an action like withdrawing funds
5. Result: Gas costs are reduced by approximately 60% compared to eager evaluation

### Example 2: Lazy Evaluation for Matured Positions

Consider a scenario with auto-rolling positions:

1. Charlie has a lending position of 2,000 USDC in the MAR2024 market
2. When MAR2024 reaches maturity:
   - Without lazy evaluation: The system would need to update all positions in the MAR2024 market, potentially thousands of transactions
   - With lazy evaluation: No immediate updates occur
3. When Charlie checks his position after maturity:
   - The system detects the maturity date has passed
   - It automatically treats the position as an Auto-rolled Position (GV)
   - It calculates the new position value based on the auto-roll price
4. When Charlie eventually withdraws or modifies his position:
   - Only then is the CleanUp process executed
   - The position is formally updated in storage
5. Result: The protocol saves massive amounts of gas by avoiding unnecessary updates to all positions at maturity

### Example 3: Gas Optimization Through Recycling

The protocol further optimizes gas usage through market recycling:

1. The protocol has 9 orderbooks for ETH (8 active, 1 inactive)
2. When the MAR2024 market matures:
   - The market contract is not discarded but recycled
   - It becomes the new inactive market (which will eventually be MAR2026)
3. This recycling process:
   - Avoids the high gas cost of deploying new contracts
   - Maintains a fixed number of markets to evaluate
   - Keeps the lazy evaluation process efficient
4. A user with positions across multiple maturities benefits from:
   - Consistent gas costs regardless of how many markets are active
   - Predictable behavior when markets mature
   - Efficient position management across the entire protocol

## FAQ

### How does Lazy Evaluation reduce gas costs?

Lazy Evaluation reduces gas costs in several ways:
1. **Deferred Storage Updates**: Instead of updating storage (which is expensive in Ethereum) every time an order is partially filled or a position changes, updates are batched and performed only when necessary.
2. **Calculation vs. Storage**: The protocol uses real-time calculations instead of storage updates whenever possible. Reading from storage is much cheaper than writing to it.
3. **Batched Operations**: Multiple changes can be combined into a single storage update when a user takes an action like withdrawing funds.
4. **Reduced Contract Calls**: By handling multiple state changes in a single operation, the number of contract calls is reduced.
5. **Optimized Auto-Roll**: The auto-roll process would be prohibitively expensive without lazy evaluation, as it would require updating every position at maturity.

### When does the CleanUp process occur?

The CleanUp process is triggered by specific user actions:
1. **Order Execution**: When a user places a new order that matches with existing orders
2. **Collateral Withdrawals**: When a user withdraws collateral from the system
3. **Position Modifications**: When a user modifies their position (e.g., adding more funds)
4. **Token Minting/Burning**: When a user mints or burns ZC tokens
5. **Manual Settlement**: When a user manually settles a position at maturity

The CleanUp process is designed to occur during operations that already require storage updates, minimizing additional gas costs.

### How does Lazy Evaluation affect the user experience?

Lazy Evaluation is designed to be transparent to users:
1. **Real-Time Information**: Users always see the current state of their positions, calculated in real-time
2. **Lower Transaction Costs**: Users pay significantly lower gas fees for transactions
3. **Faster Transactions**: With fewer storage operations, transactions confirm more quickly
4. **Seamless Auto-Roll**: Users don't need to manually roll over positions at maturity
5. **No Action Required**: Users don't need to take any special actions to benefit from lazy evaluation

The system handles all the complexity behind the scenes, providing users with an intuitive experience while optimizing for gas efficiency.

### Can Lazy Evaluation lead to inconsistencies in the system?

No, Lazy Evaluation is designed to maintain complete consistency:
1. **Deterministic Calculations**: All calculations are deterministic and will produce the same result regardless of when they're performed
2. **Smart Contract Guarantees**: The smart contract ensures that lazy calculations always reflect the true state
3. **Eventual Consistency**: While updates may be deferred, the system will always reach a consistent state
4. **Validation Checks**: The protocol includes validation checks to ensure that lazy evaluation doesn't introduce inconsistencies
5. **Formal Verification**: The lazy evaluation mechanism has been formally verified to ensure correctness

The protocol prioritizes both efficiency and correctness, ensuring that lazy evaluation never compromises the integrity of the system.

### How does Lazy Evaluation interact with the Red-Black Tree data structure?

The Red-Black Tree and Lazy Evaluation work together to optimize the orderbook:
1. **Efficient Order Management**: The Red-Black Tree provides O(log n) operations for order insertion and deletion
2. **Unlink Operation**: When an order is filled, it's "unlinked" from the tree rather than immediately removed
3. **Deferred Cleanup**: The actual removal of unlinked nodes happens during the CleanUp process
4. **Optimized Traversal**: When searching the tree, unlinked nodes are skipped, maintaining efficient operations
5. **Complementary Optimizations**: Both mechanisms work together to minimize gas costs while maintaining performance

This combination of data structures and evaluation strategies is what enables the protocol to achieve its high efficiency.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Order States | Number of possible states for orders in the system | 3 (Open Order, Active Position, Auto-rolled Position) |
| CleanUp Trigger | Operations that trigger the CleanUp process | Order execution, collateral withdrawals, etc. |
| Calculation Timing | When actual values are calculated | Real-time, only when requested |
| Storage Optimization | How storage is optimized for gas efficiency | Recycling of mature market contracts |
| Evaluation Method | How order and position values are determined | Deferred until necessary |
| Gas Savings | Typical gas savings compared to eager evaluation | 40-60% |
| Maximum Orderbooks | Maximum number of orderbooks per currency | 9 (8 active, 1 inactive) |
| State Transition | When positions transition between states | At maturity or when orders are filled |

## Related Resources

- [Orderbook Deep Dive](README.md)
- [Genesis Value](genesis-value.md)
- [Compound Factor](compound-factor.md)
- [Orderbook Rotation](orderbook-rotation.md)
- [Red-Black Tree](red-black-tree.md)
- [Gas Cost](../../../resources/knowledge-base/gas-cost.md)
