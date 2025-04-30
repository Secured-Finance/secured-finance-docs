---
description: API Reference for Secured Finance protocols
---

# 🔌 API Reference

Secured Finance provides GraphQL APIs via The Graph protocol to query data from our smart contracts. This section documents how to use these APIs to access data from our protocols.

## What You'll Learn

* How to query data from the Fixed-Rate Lending protocol
* Examples of common queries and their responses
* How to use GraphQL to build custom queries
* How to use our interactive API documentation with "Test It" functionality

## Key Components

### Subgraphs

Secured Finance maintains subgraphs for its protocols:

* [Fixed-Rate Lending Subgraph](fixed-rate-lending-subgraph/) - For querying data from the Fixed-Rate Lending protocol

> **Note:** The USDFC Subgraph is currently under development and not yet deployed. USDFC data is only available through the [USDFC SDK](../sdk-reference/usdfc-sdk.md).

### Available Networks

Our subgraphs are deployed on the following networks:

| Protocol           | Ethereum | Arbitrum | Filecoin |
| ------------------ | -------- | -------- | -------- |
| USDFC              |          |          |          |
| Fixed-Rate Lending | ✅        | ✅        | ✅        |

> **Note:** The USDFC Subgraph is not deployed on any network yet. USDFC data is only available through the [USDFC SDK](../sdk-reference/usdfc-sdk.md).

### Subgraph Endpoints

#### Fixed-Rate Lending Subgraph

**Ethereum**

* Mainnet: [https://api.studio.thegraph.com/query/64582/sf-prd-mainnet/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-mainnet/version/latest)
* Sepolia: [https://api.studio.thegraph.com/query/64582/sf-prd-sepolia/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-sepolia/version/latest)

**Arbitrum**

* Mainnet: [https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-one/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-one/version/latest)
* Sepolia: [https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-sepolia/version/latest](https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-sepolia/version/latest)

**Filecoin**

> **Note:** The Filecoin subgraph endpoints are currently under development. Please check back later for updated URLs.

## Getting Started

If you're new to GraphQL or The Graph, check out our introduction to subgraphs in the next sections. If you're already familiar with these technologies, you can jump directly to the specific subgraph documentation.

The Graph is a decentralized protocol for indexing and querying blockchain data, making it easier to query the difficult-to-read data stored on the blockchain. The Graph's decentralized approach ensures resilience, eliminating the need for centralized and resource-intensive alternatives.

To view the source of our subgraphs, visit our [GitHub Repository](https://github.com/Secured-Finance/secured-finance-subgraph).

## Interactive API Documentation

We provide interactive API documentation for our Fixed-Rate Lending Subgraph using GitBook's OpenAPI integration. This allows you to explore and test the API directly from the documentation page in real-time.

{% openapi-operation path="./fixed-rate-lending-subgraph/openapi.yaml" method="post" %}
[Fixed-Rate Lending Subgraph API Documentation]
{% endopenapi-operation %}

The interactive documentation above allows you to:

1. Explore available endpoints and operations
2. View request and response schemas
3. Try out API calls directly from the documentation using the "Test It" feature
4. See example queries and responses

### Using the Interactive Documentation

1. Browse through the available operations
2. Click on an operation to expand it
3. View the request parameters and example values
4. Click "Test It" to execute a request against the selected server
5. View the response directly in the documentation

For more complex queries, you can also use The Graph's Playground interface by visiting the subgraph endpoints directly.

## Related Resources

* [The Graph Documentation](https://thegraph.com/docs/en/)
* [GraphQL Documentation](https://graphql.org/learn/)
* [Secured Finance GitHub Repositories](https://github.com/Secured-Finance)
