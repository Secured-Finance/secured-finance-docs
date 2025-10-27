---
description: Example queries for the USDFC Subgraph
---

# 🔍 Query Examples

This page provides examples of common queries for the USDFC Subgraph to help you get started.

## Basic Queries

### Get Protocol Overview
Retrieve system-wide statistics:

```graphql
{
  global(id: "only") {
    totalCollateral
    totalDebt
    troveCount
    borrowingFee
    redemptionFee
    stabilityPoolUSDFCDeposit
    systemCollateralRatio
  }
}
```

### Get User Information
Query a user's Troves and stability deposits:

```graphql
{
  user(id: "0x123...") {
    id
    troves {
      id
      collateral
      debt
      collateralRatio
      status
    }
    stabilityDeposits {
      id
      amount
    }
  }
}
```

### List Active Troves
Get a list of active Troves with their details:

```graphql
{
  troves(
    where: { status: ACTIVE },
    orderBy: collateralRatio,
    orderDirection: asc,
    first: 10
  ) {
    id
    owner {
      id
    }
    collateral
    debt
    collateralRatio
    status
    createdAt
  }
}
```

## Advanced Queries

### Monitor Liquidation Events
Retrieve recent liquidation events:

```graphql
{
  liquidations(
    orderBy: timestamp,
    orderDirection: desc,
    first: 20
  ) {
    id
    user {
      id
    }
    trove {
      id
    }
    liquidatedCollateral
    liquidatedDebt
    timestamp
  }
}
```

### Track Redemption Activity
Query recent redemption events:

```graphql
{
  redemptions(
    orderBy: timestamp,
    orderDirection: desc,
    first: 10
  ) {
    id
    user {
      id
    }
    amountRedeemed
    collateralRedeemed
    fee
    timestamp
  }
}
```

### Get Price Feed Updates
Track price feed updates over time:

```graphql
{
  priceFeedUpdates(
    orderBy: timestamp,
    orderDirection: desc,
    first: 20
  ) {
    id
    price
    timestamp
  }
}
```

## Historical Analysis

### Calculate System Stability
Monitor system collateral ratio over time:

```graphql
{
  systemStates(
    orderBy: timestamp,
    orderDirection: desc,
    first: 30
  ) {
    id
    totalCollateral
    totalDebt
    systemCollateralRatio
    timestamp
  }
}
```

### Track Trove Changes
Follow the history of a specific Trove:

```graphql
{
  troveOperations(
    where: { trove: "0x456..." },
    orderBy: timestamp,
    orderDirection: asc
  ) {
    id
    trove {
      id
    }
    operation
    collateralChange
    debtChange
    timestamp
  }
}
```

## Real-time Monitoring

### Subscriptions
Use GraphQL subscriptions to monitor events in real-time:

```graphql
subscription {
  troveOperation(orderBy: timestamp, orderDirection: desc) {
    id
    trove {
      id
      owner {
        id
      }
    }
    operation
    collateralChange
    debtChange
    timestamp
  }
}
```

## Integration Tips

- Use the `first` and `skip` parameters for pagination
- Use `orderBy` and `orderDirection` to sort results
- Use `where` filters to narrow down the data
- For time-series data, use `timestamp_gt` and `timestamp_lt` filters
- Connect to the specific network endpoint (Ethereum, Arbitrum, or Filecoin) based on your application needs

## JavaScript Example

Here's how to query the USDFC Subgraph using JavaScript and the Apollo Client:

```javascript
import { ApolloClient, InMemoryCache, gql } from '@apollo/client';

// Initialize Apollo Client
const client = new ApolloClient({
  uri: 'https://api.thegraph.com/subgraphs/name/secured-finance/usdfc-filecoin',
  cache: new InMemoryCache()
});

// Query example
async function getProtocolOverview() {
  const { data } = await client.query({
    query: gql`
      {
        global(id: "only") {
          totalCollateral
          totalDebt
          troveCount
          systemCollateralRatio
        }
      }
    `
  });
  
  console.log('Protocol Overview:', data.global);
  return data.global;
}

getProtocolOverview();
```

This will output the current state of the USDFC protocol including total collateral, debt, and number of Troves.
