---
description: Example queries for the Fixed-Rate Lending Subgraph
---

# 🔍 Query Examples

The Graph uses the GraphQL language to query the subgraphs. This doc will teach you how to query the Secured Finance Subgraphs by writing the GraphQL queries. You can copy and paste these queries into the [Subgraph endpoints](README.md#subgraph-endpoints).

### Tips and Guidelines:

* Ensure that all address values (used for id) are in lowercase format.
* Be aware of the units for each asset while querying. These fields will be returned in the decimals of the asset itself(e.g., 10^18 for Ether, 10^6 for USDC).
* Each results page defaults to returning 100 entries. If needed, you can increase this limit to a maximum of 1000 entries per page by passing the `first` parameter.
* To query for groups of entities in the middle of a collection, use the `skip` parameter in conjunction with the `first` parameter to skip a specified number of entities starting at the beginning of the collection.
* For large datasets, consider optimising queries by fetching only the necessary fields and using pagination effectively.
* Use the `orderBy` parameter to sort by a specific attribute and the `orderDirection` for ascending (`asc`) or descending(`desc`) direction.
* Use the `where` parameter to filter for specific properties.

### Order Entity

When a user places an order on our protocol, it is stored in the Order entity. You can check the order entity [here](https://github.com/Secured-Finance/secured-finance-subgraph/blob/develop/schema.graphql#L22).

```graphql
{
  orders(where: {user: "0xe477f1adcd3b4a2e1e152f79105a18e5368f0d33"}) {
    orderId
    user {
      id
    }
    side
    currency
    maturity
    status
    filledAmount
    inputAmount
    inputUnitPrice
    type
    isPreOrder
  }
}
```

### Transfer Entity

When a user deposits or withdraws assets, it is stored in the Transfer entity. You can check the Transfer entity [here](https://github.com/Secured-Finance/secured-finance-subgraph/blob/develop/schema.graphql#L170).

```graphql
{
  transfers(where: {user: "0xe477f1adcd3b4a2e1e152f79105a18e5368f0d33"}) {
    user {
      id
    }
    currency
    amount
    transferType
    timestamp
    blockNumber
    txHash
  }
}
```

### Liquidation Entity

When a user is liquidated, it is stored in the Liquidation entity. You can check the Liquidation entity [here](https://github.com/Secured-Finance/secured-finance-subgraph/blob/develop/schema.graphql#L153).

```graphql
{
  liquidations(where: {user: "0xe477f1adcd3b4a2e1e152f79105a18e5368f0d33"}) {
    user {
      id
    }
    collateralCurrency
    debtCurrency
    debtMaturity
    debtAmount
    timestamp
    blockNumber
    txHash
  }
}
```

### Transaction Entity

When a user takes an order or its order is taken, it is stored in the Transaction entity. You can check the Transaction entity [here](https://github.com/Secured-Finance/secured-finance-subgraph/blob/develop/schema.graphql#L1).

```graphql
{
  transactions(where: {user: "0xe477f1adcd3b4a2e1e152f79105a18e5368f0d33"}) {
    user {
      id
    }
    currency
    maturity
    side
    executionPrice
    executionType
    futureValue
    amount
    feeInFV
    averagePrice
    lendingMarket {
      id
    }
    order {
      id
      orderId
    }
    createdAt
    blockNumber
    txHash
  }
}
```

### User Entity

All users' information for their orders, transactions, transfers, liquidations etc. are stored in the User entity. You can check the User entity [here](https://github.com/Secured-Finance/secured-finance-subgraph/blob/develop/schema.graphql#L80).

```graphql
{
  user (id: "0xe477f1adcd3b4a2e1e152f79105a18e5368f0d33") {
    id
    createdAt
    transactionCount
    orderCount
    liquidationCount
    transferCount
    orders (orderBy: orderId, orderDirection: asc) {
      orderId
      currency
      maturity
      status
      inputAmount
      inputUnitPrice
    }
    transactions (skip: 20, first: 20) {
      currency
      maturity
      amount
      executionType
    }
    liquidations (where: {debtCurrency: "0x4554480000000000000000000000000000000000000000000000000000000000"}, orderBy: debtAmount, orderDirection: desc) {
      debtCurrency
      debtMaturity
      debtAmount
    }
    transfers (where: {transferType: Deposit}) {
      currency
      amount
      transferType
    }
    deposits {
      currency
      amount
    }
    takerVolumesByCurrency {
      currency
      totalVolume
    }
  }
}
```

You can also add nested filtering in the queries. The below query will fetch the users and their orders list where orderId is 1.

```graphql
{
  users (where: { orders_: {orderId: 1}}) {
    id
    orders (where: {orderId: 1}) {
      orderId
      currency
      maturity
      status
      inputAmount
      inputUnitPrice
      type
      isPreOrder
    }
  }
}
```
