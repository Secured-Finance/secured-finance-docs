# Query Examples

This page provides examples of GraphQL queries that can be used with our subgraphs.

## Basic Queries

### Get All Markets

```graphql
{
  markets {
    id
    name
    baseToken {
      id
      name
      symbol
      decimals
    }
    quoteToken {
      id
      name
      symbol
      decimals
    }
    maturity
    createdAtTimestamp
    createdAtBlockNumber
  }
}
```

### Get Market by ID

```graphql
{
  market(id: "0x...") {
    id
    name
    baseToken {
      id
      name
      symbol
      decimals
    }
    quoteToken {
      id
      name
      symbol
      decimals
    }
    maturity
    createdAtTimestamp
    createdAtBlockNumber
  }
}
```

## Order Queries

### Get All Orders

```graphql
{
  orders(first: 10) {
    id
    market {
      id
      name
    }
    maker
    price
    amount
    side
    status
    createdAtTimestamp
    createdAtBlockNumber
  }
}
```

### Get Orders by User

```graphql
{
  orders(where: {maker: "0x..."}) {
    id
    market {
      id
      name
    }
    price
    amount
    side
    status
    createdAtTimestamp
    createdAtBlockNumber
  }
}
```

## Trade Queries

### Get Recent Trades

```graphql
{
  trades(first: 10, orderBy: createdAtTimestamp, orderDirection: desc) {
    id
    market {
      id
      name
    }
    maker
    taker
    price
    amount
    createdAtTimestamp
    createdAtBlockNumber
  }
}
```

### Get Trades by Market

```graphql
{
  trades(where: {market: "0x..."}) {
    id
    maker
    taker
    price
    amount
    createdAtTimestamp
    createdAtBlockNumber
  }
}
```

## Position Queries

### Get User Positions

```graphql
{
  positions(where: {user: "0x..."}) {
    id
    user
    market {
      id
      name
    }
    collateralToken {
      id
      symbol
    }
    collateralAmount
    debtToken {
      id
      symbol
    }
    debtAmount
    createdAtTimestamp
    updatedAtTimestamp
  }
}
```

## Historical Data Queries

### Get Price History for a Market

```graphql
{
  trades(
    where: {market: "0x..."}
    orderBy: createdAtTimestamp
    orderDirection: asc
  ) {
    price
    amount
    createdAtTimestamp
  }
}
```

## Advanced Queries

### Get Market Statistics

```graphql
{
  marketDayData(id: "0x...-1234567") {
    id
    date
    market {
      id
      name
    }
    volumeUSD
    txCount
    openInterestUSD
    liquidityUSD
  }
}
```

### Get Protocol Statistics

```graphql
{
  securedFinanceDayData(id: "1234567") {
    id
    date
    totalVolumeUSD
    totalLiquidityUSD
    totalOpenInterestUSD
    txCount
  }
}
```

These examples should help you get started with querying our subgraphs. You can modify these queries to suit your specific needs or combine them to create more complex queries.
