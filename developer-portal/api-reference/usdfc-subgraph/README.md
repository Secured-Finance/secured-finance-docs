---
description: Documentation for querying the USDFC Subgraph
---

# 📈 USDFC Subgraph

The USDFC Subgraph indexes data from the USDFC stablecoin protocol, allowing developers to query historical and current data using GraphQL.

## Overview

USDFC is a collateralized debt platform built on the Filecoin blockchain. Users can lock up FIL as collateral and issue USDFC stablecoin tokens. The USDFC Subgraph provides a way to query information about Troves (collateralized positions), stability deposits, redemptions, liquidations, and other protocol activities.

## How It Works

The USDFC Subgraph continuously indexes events emitted by the USDFC smart contracts. This data is organized into entities that can be queried using GraphQL. The subgraph provides real-time access to protocol data without requiring direct interaction with the blockchain.

## Subgraph Endpoints

Access the USDFC Subgraph through these endpoints:

| Network | URL |
|---------|-----|
| Ethereum | https://api.thegraph.com/subgraphs/name/secured-finance/usdfc-ethereum |
| Arbitrum | https://api.thegraph.com/subgraphs/name/secured-finance/usdfc-arbitrum |
| Filecoin | https://api.thegraph.com/subgraphs/name/secured-finance/usdfc-filecoin |

## Key Entities

The USDFC Subgraph schema includes these primary entities:

### User

Represents users who interact with the USDFC protocol.

```graphql
type User @entity {
  id: ID!
  troves: [Trove!]! @derivedFrom(field: "owner")
  stabilityDeposits: [StabilityDeposit!]! @derivedFrom(field: "owner")
  liquidations: [Liquidation!]! @derivedFrom(field: "user")
  redemptions: [Redemption!]! @derivedFrom(field: "user")
}
```

### Trove

Represents a collateralized debt position in the USDFC protocol.

```graphql
type Trove @entity {
  id: ID!
  owner: User!
  collateral: BigDecimal!
  debt: BigDecimal!
  collateralRatio: BigDecimal
  status: TroveStatus!
  createdAt: BigInt!
  updatedAt: BigInt!
}

enum TroveStatus {
  ACTIVE
  CLOSED
  LIQUIDATED
  REDEEMED
}
```

### StabilityDeposit

Represents a deposit in the Stability Pool.

```graphql
type StabilityDeposit @entity {
  id: ID!
  owner: User!
  amount: BigDecimal!
  createdAt: BigInt!
  updatedAt: BigInt!
}
```

### Liquidation

Records details of a liquidation event.

```graphql
type Liquidation @entity {
  id: ID!
  user: User!
  trove: Trove!
  liquidatedCollateral: BigDecimal!
  liquidatedDebt: BigDecimal!
  collateralGasCompensation: BigDecimal!
  debtGasCompensation: BigDecimal!
  timestamp: BigInt!
}
```

### Redemption

Records details of a redemption event.

```graphql
type Redemption @entity {
  id: ID!
  user: User!
  amountRedeemed: BigDecimal!
  collateralRedeemed: BigDecimal!
  fee: BigDecimal!
  timestamp: BigInt!
}
```

## Examples

See the [Query Examples](query-examples.md) page for sample queries to get started.

## OpenAPI Interactive Documentation

You can interact with the USDFC Subgraph directly through GraphQL using The Graph's Playground. Click the links below to access the interactive interface:

- [Ethereum Playground](https://thegraph.com/hosted-service/subgraph/secured-finance/usdfc-ethereum)
- [Arbitrum Playground](https://thegraph.com/hosted-service/subgraph/secured-finance/usdfc-arbitrum)
- [Filecoin Playground](https://thegraph.com/hosted-service/subgraph/secured-finance/usdfc-filecoin)

## FAQ

### How do I query the total collateral in the system?
Use the global entity to query system-wide statistics:

```graphql
{
  global(id: "only") {
    totalCollateral
    totalDebt
    troveCount
  }
}
```

### How can I monitor liquidation events?
Subscribe to liquidation events using a subscription query:

```graphql
subscription {
  liquidation(orderBy: timestamp, orderDirection: desc) {
    id
    user { id }
    liquidatedCollateral
    liquidatedDebt
    timestamp
  }
}
```

### Does the subgraph support pagination?
Yes, use the first, skip, and orderBy parameters to paginate through results:

```graphql
{
  troves(
    first: 10,
    skip: 20,
    orderBy: collateralRatio,
    orderDirection: asc
  ) {
    id
    owner { id }
    collateral
    debt
    collateralRatio
  }
}
```

## Related Resources
- [USDFC Protocol Documentation](../../usdfc-stablecoin/overview.md)
- [USDFC SDK Documentation](../sdk-reference/usdfc-sdk.md)
- [GitHub Repository](https://github.com/Secured-Finance/stablecoin-contracts)
