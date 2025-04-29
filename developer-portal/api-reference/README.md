---
description: API Reference for Secured Finance protocols
---

# 🔌 API Reference

Secured Finance provides GraphQL APIs via The Graph protocol to query data from our smart contracts. This section documents how to use these APIs to access data from our protocols.

## What You'll Learn

- How to query data from the USDFC stablecoin protocol
- How to query data from the Fixed-Rate Lending protocol
- Examples of common queries and their responses
- How to use GraphQL to build custom queries

## Key Components

### Subgraphs

Secured Finance maintains subgraphs for each of its protocols:

- [USDFC Subgraph](usdfc-subgraph/README.md) - For querying data from the USDFC stablecoin protocol
- [Fixed-Rate Lending Subgraph](fixed-rate-lending-subgraph/README.md) - For querying data from the Fixed-Rate Lending protocol

### Available Networks

Our subgraphs are deployed on multiple networks:

| Protocol | Ethereum | Arbitrum | Filecoin |
|----------|----------|----------|----------|
| USDFC | ✅ | ✅ | ✅ |
| Fixed-Rate Lending | ✅ | ✅ | ✅ |

### Subgraph Endpoints

#### Fixed-Rate Lending Subgraph

##### Ethereum
* Mainnet: [https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-mainnet/0.0.3](https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-mainnet/0.0.3)
* Sepolia: [https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-sepolia/0.0.3](https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-sepolia/0.0.3)

##### Arbitrum
* Mainnet: [https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-arbitrum/0.0.3](https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-arbitrum/0.0.3)
* Sepolia: [https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-arbitrum-sepolia/0.0.3](https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-arbitrum-sepolia/0.0.3)

##### Filecoin
* Mainnet: [https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-filecoin/0.0.3](https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-filecoin/0.0.3)
* Calibration: [https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-filecoin-calibration/0.0.3](https://api.studio.thegraph.com/proxy/61214/sf-protocol-prd-filecoin-calibration/0.0.3)

## Getting Started

If you're new to GraphQL or The Graph, check out our introduction to subgraphs in the next sections. If you're already familiar with these technologies, you can jump directly to the specific subgraph documentation.

The Graph is a decentralized protocol for indexing and querying blockchain data, making it easier to query the difficult-to-read data stored on the blockchain. The Graph's decentralized approach ensures resilience, eliminating the need for centralized and resource-intensive alternatives.

To view the source of our subgraphs, visit our [GitHub Repository](https://github.com/Secured-Finance/secured-finance-subgraph).

## OpenAPI Integration

GitBook supports OpenAPI specifications, allowing you to create interactive API documentation. To add an OpenAPI spec to your documentation:

1. Create an OpenAPI specification file (in JSON or YAML format)
2. In GitBook, navigate to the page where you want to add the API reference
3. Click on the "+" button and select "API Reference"
4. Upload your OpenAPI specification file or provide a URL to the file
5. Configure the display options as needed

For our subgraphs, you can use the GraphQL schema as the basis for creating an OpenAPI specification. The Graph also provides a GraphQL Playground interface that allows for interactive querying.

### Example OpenAPI Integration

```yaml
openapi: 3.0.0
info:
  title: Secured Finance API
  version: 1.0.0
  description: API for interacting with Secured Finance protocols
paths:
  /subgraphs/name/secured-finance/fixed-rate-lending-filecoin:
    post:
      summary: Query the Fixed-Rate Lending Subgraph
      description: Execute a GraphQL query against the Fixed-Rate Lending Subgraph
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                query:
                  type: string
                  example: |
                    {
                      orders(first: 10) {
                        id
                        side
                        amount
                        price
                        status
                      }
                    }
                variables:
                  type: object
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: object
```

## Related Resources

- [The Graph Documentation](https://thegraph.com/docs/en/)
- [GraphQL Documentation](https://graphql.org/learn/)
- [Secured Finance GitHub Repositories](https://github.com/Secured-Finance)
