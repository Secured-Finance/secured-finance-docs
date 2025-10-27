---
description: Documentation for querying the Fixed-Rate Lending Subgraph
---

# 📈 Fixed-Rate Lending Subgraph

The Fixed-Rate Lending Subgraph indexes data from the Secured Finance Fixed-Rate Lending protocol, enabling developers to query historical and current data using GraphQL.

## Overview

The Fixed-Rate Lending protocol provides a platform for fixed-rate lending and borrowing through an order book system. The subgraph allows you to query information about orders, lending markets, transactions, positions, and other protocol activities.

## How It Works

The Fixed-Rate Lending Subgraph continuously indexes events emitted by the Fixed-Rate Lending smart contracts. This data is organized into entities that can be queried using GraphQL, providing real-time access to protocol data without requiring direct interaction with the blockchain.

## Subgraph Endpoints

For the complete list of subgraph endpoints, please refer to the [API Reference](../README.md#subgraph-endpoints) page.

You can access the Fixed-Rate Lending Subgraph through these endpoints:

- Ethereum Mainnet: [https://api.studio.thegraph.com/query/64582/sf-prd-mainnet/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-mainnet/version/latest)
- Ethereum Sepolia: [https://api.studio.thegraph.com/query/64582/sf-prd-sepolia/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-sepolia/version/latest)
- Arbitrum One: [https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-one/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-one/version/latest)
- Arbitrum Sepolia: [https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-sepolia/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-sepolia/version/latest)

> **Note:** The Filecoin subgraph endpoints are currently under development. Please check back later for updated URLs.

## Key Entities

The Fixed-Rate Lending Subgraph schema includes these primary entities:

### Transaction

Represents a transaction on the Fixed-Rate Lending protocol.

```graphql
type Transaction @entity {
  id: ID!
  currency: Bytes!
  maturity: BigInt!
  side: Int!
  executionPrice: BigInt!
  user: User!
  executionType: TransactionExecutionType!
  futureValue: BigInt!
  amount: BigInt!
  feeInFV: BigInt!
  averagePrice: BigDecimal!
  lendingMarket: LendingMarket!
  order: Order!
  createdAt: BigInt!
  blockNumber: BigInt!
  txHash: Bytes!
}

enum TransactionExecutionType {
  Maker
  Taker
}
```

### User

Represents users who interact with the Fixed-Rate Lending protocol.

```graphql
type User @entity {
  id: ID! # wallet address
  createdAt: BigInt!
  transactionCount: BigInt!
  transactions: [Transaction!]! @derivedFrom(field: "user")
  orderCount: BigInt!
  orders: [Order!]! @derivedFrom(field: "user")
  liquidationCount: BigInt!
  liquidations: [Liquidation!]! @derivedFrom(field: "user")
  transferCount: BigInt!
  transfers: [Transfer!]! @derivedFrom(field: "user")
  deposits: [Deposit!]! @derivedFrom(field: "user")
  takerVolumesByCurrency: [TakerVolumeByCurrency!]! @derivedFrom(field: "user")
}
```

### Order

Represents an order in the order book.

```graphql
type Order @entity {
  id: ID!
  orderId: BigInt!
  user: User!
  currency: Bytes!
  side: Int!
  maturity: BigInt!
  inputUnitPrice: BigInt!
  inputAmount: BigInt!
  filledAmount: BigInt!
  status: OrderStatus!
  statusUpdatedAt: BigInt!
  lendingMarket: LendingMarket!
  isPreOrder: Boolean!
  type: OrderType!
  transactions: [Transaction!]! @derivedFrom(field: "order")
  isCircuitBreakerTriggered: Boolean!
  createdAt: BigInt!
  blockNumber: BigInt!
  txHash: Bytes!
}

enum OrderType {
  Market
  Limit
  Unwind
}

enum OrderStatus {
  Open
  PartiallyFilled
  Filled
  Killed
  Cancelled
}
```

### LendingMarket

Represents a lending market for a specific currency and maturity.

```graphql
type LendingMarket @entity {
  id: ID!
  currency: Bytes!
  maturity: BigInt!
  isActive: Boolean!
  transactions: [Transaction!]! @derivedFrom(field: "lendingMarket")
  orders: [Order!]! @derivedFrom(field: "lendingMarket")
  volume: BigInt!
  dailyVolume: [DailyVolume!]! @derivedFrom(field: "lendingMarket")
  openingUnitPrice: BigInt!
  lastLendUnitPrice: BigInt!
  lastBorrowUnitPrice: BigInt!
  offsetAmount: BigInt!
}
```

### Liquidation

Records details of a liquidation event.

```graphql
type Liquidation @entity {
  id: ID!
  collateralCurrency: Bytes!
  debtCurrency: Bytes!
  debtMaturity: BigInt!
  debtAmount: BigInt!
  user: User!
  timestamp: BigInt!
  blockNumber: BigInt!
  txHash: Bytes!
}
```

### Transfer

Records details of a deposit or withdrawal.

```graphql
type Transfer @entity {
  id: ID!
  user: User!
  currency: Bytes!
  amount: BigInt!
  transferType: TransferType!
  timestamp: BigInt!
  blockNumber: BigInt!
  txHash: Bytes!
}

enum TransferType {
  Deposit
  Withdraw
}
```

### Deposit

Records details of a user's deposit.

```graphql
type Deposit @entity {
  id: ID!
  user: User!
  currency: Bytes!
  amount: BigInt!
}
```

### DailyVolume

Records daily trading volume for a lending market.

```graphql
type DailyVolume @entity {
  id: ID! # currency-maturity-date(yyyy-mm-dd)
  currency: Bytes!
  maturity: BigInt!
  day: String! # dd-mm-yyyy
  volume: BigInt!
  timestamp: BigInt!
  lendingMarket: LendingMarket!
}
```

### Protocol

Records protocol-wide statistics.

```graphql
type Protocol @entity {
  id: ID! # 1
  totalUsers: BigInt!
  volumesByCurrency: [ProtocolVolumeByCurrency!]! @derivedFrom(field: "protocol")
}
```

### ProtocolVolumeByCurrency

Records total volume by currency for the protocol.

```graphql
type ProtocolVolumeByCurrency @entity {
  id: ID! # currency
  protocol: Protocol!
  currency: Bytes!
  totalVolume: BigInt!
}
```

### TakerVolumeByCurrency

Records taker volume by currency for a user.

```graphql
type TakerVolumeByCurrency @entity {
  id: ID! # user-currency
  user: User!
  currency: Bytes!
  totalVolume: BigInt!
  totalVolumesByInterval: [TakerVolumeByIntervalAndCurrency!]! @derivedFrom(field: "takerVolumesByCurrency")
}
```

### TransactionCandleStick

Records price candles for transactions.

```graphql
type TransactionCandleStick @entity {
  id: ID! # A composite ID, e.g., "currency-maturity-interval-epochTime"
  interval: BigInt! # interval in seconds
  currency: Bytes!
  maturity: BigInt!
  timestamp: BigInt! # The start time of the interval
  open: BigInt!
  close: BigInt!
  high: BigInt!
  low: BigInt!
  average: BigDecimal!
  volume: BigInt!
  volumeInFV: BigInt!
  lendingMarket: LendingMarket!
}
```

### TakerVolumeByIntervalAndCurrency

Records taker volume by interval and currency.

```graphql
type TakerVolumeByIntervalAndCurrency @entity {
  id: ID! # Composite ID, e.g., "user-currency-interval-createdAt"
  takerVolumesByCurrency: TakerVolumeByCurrency!
  currency: Bytes!
  interval: BigInt!
  createdAt: BigInt! # The start time of the interval
  volume: BigInt! # Total transaction volume for the interval
  updatedAt: BigInt! # Timestamp when the record was last updated
}
```

## Examples

See the [Query Examples](query-examples.md) page for sample queries to get started.

## Interactive Documentation

You can interact with the Fixed-Rate Lending Subgraph directly through GraphQL using The Graph's Playground by visiting the subgraph endpoints listed above.

For interactive API documentation embedded directly in this documentation, please refer to the [API Reference](../README.md#interactive-api-documentation) page.

## FAQ

### How do I query all active orders for a specific market?
Use the orders entity with filters:

```graphql
{
  orders(
    where: {
      lendingMarket: "0x123...",
      status_in: [Open, PartiallyFilled]
    }
  ) {
    id
    user { id }
    side
    inputAmount
    inputUnitPrice
    status
  }
}
```

### How can I monitor new lending markets?
Subscribe to lending market events:

```graphql
subscription {
  lendingMarket(orderBy: maturity, orderDirection: desc) {
    id
    currency
    maturity
    isActive
    lastLendUnitPrice
    lastBorrowUnitPrice
  }
}
```

### How do I calculate APR from unit prices?
The unit price in the Fixed-Rate Lending protocol represents a percentage of par value. To convert to APR:

$$
APR = \left(\frac{10000}{unitPrice} - 1\right) \times \frac{365}{daysToMaturity} \times 100\%
$$

## Related Resources
- [Fixed-Rate Lending Protocol Documentation](../../fixed-rate-lending/overview/README.md)
- [Fixed-Rate Lending SDK Documentation](../sdk-reference/fixed-rate-lending-sdk.md)
- [GitHub Repository](https://github.com/Secured-Finance/secured-finance-subgraph)

