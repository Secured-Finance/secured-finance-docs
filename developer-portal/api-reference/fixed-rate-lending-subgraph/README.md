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
  blockNumber: BigInt!
  timestamp: BigInt!
  from: Bytes!
  gasPrice: BigInt
  gasUsed: BigInt
  gasLimit: BigInt
  status: TransactionStatus
}

enum TransactionStatus {
  PENDING
  SUCCESS
  FAILED
}
```

### User

Represents users who interact with the Fixed-Rate Lending protocol.

```graphql
type User @entity {
  id: ID!
  transactions: [Transaction!]! @derivedFrom(field: "user")
  orders: [Order!]! @derivedFrom(field: "user")
  positions: [Position!]! @derivedFrom(field: "user")
}
```

### Order

Represents an order in the order book.

```graphql
type Order @entity {
  id: ID!
  user: User!
  market: LendingMarket!
  side: OrderSide!
  amount: BigInt!
  price: BigInt!
  status: OrderStatus!
  createdAt: BigInt!
  executedAt: BigInt
  cancelledAt: BigInt
}

enum OrderSide {
  LEND
  BORROW
}

enum OrderStatus {
  PENDING
  EXECUTED
  PARTIALLY_EXECUTED
  CANCELLED
}
```

### LendingMarket

Represents a lending market for a specific currency and maturity.

```graphql
type LendingMarket @entity {
  id: ID!
  currency: Bytes!
  maturity: BigInt!
  orders: [Order!]! @derivedFrom(field: "market")
  positions: [Position!]! @derivedFrom(field: "market")
  lastPrice: BigInt
  bestLendUnitPrice: BigInt
  bestBorrowUnitPrice: BigInt
  openingDate: BigInt!
  isReady: Boolean!
}
```

### Position

Represents a user's position in a lending market.

```graphql
type Position @entity {
  id: ID!
  user: User!
  market: LendingMarket!
  side: OrderSide!
  amount: BigInt!
  presentValue: BigInt!
  createdAt: BigInt!
  updatedAt: BigInt!
}
```

### Currency

Represents a currency supported by the protocol.

```graphql
type Currency @entity {
  id: ID!
  symbol: String!
  name: String!
  decimals: Int!
  markets: [LendingMarket!]! @derivedFrom(field: "currency")
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
      market: "0x123...",
      status_in: [PENDING, PARTIALLY_EXECUTED]
    }
  ) {
    id
    user { id }
    side
    amount
    price
    status
  }
}
```

### How can I monitor new lending markets?
Subscribe to lending market events:

```graphql
subscription {
  lendingMarket(orderBy: openingDate, orderDirection: desc) {
    id
    currency
    maturity
    openingDate
    isReady
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

