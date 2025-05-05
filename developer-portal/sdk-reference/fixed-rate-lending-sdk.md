---
description: Documentation for the Fixed-Rate Lending SDK
---

# ⛽ Fixed-Rate Lending SDK

The Fixed-Rate Lending SDK is a comprehensive toolkit for developers to integrate and interact with the Secured Finance Fixed-Rate Lending protocol.

## Overview

The Fixed-Rate Lending protocol provides a platform for fixed-rate lending and borrowing through an order book system. The SDK provides a programmatic interface to interact with the protocol, allowing developers to build applications that leverage Fixed-Rate Lending functionality.

## How It Works

The Fixed-Rate Lending SDK is built on top of viem and provides a type-safe interface to interact with the Fixed-Rate Lending smart contracts. It abstracts away the complexity of direct contract interactions and provides a more developer-friendly API.

## Installation

The Fixed-Rate Lending SDK packages are hosted on GitHub Packages registry, not the public NPM registry. You'll need to configure your `.npmrc` file to access them:

```bash
# Add this to your .npmrc file
@secured-finance:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN

# Then install the individual packages
npm install @secured-finance/sf-client
npm install @secured-finance/sf-graph-client
npm install @secured-finance/sf-core
```

For more details on setting up authentication for GitHub Packages, see the [GitHub documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry#authenticating-to-github-packages).


## Key Components

The Fixed-Rate Lending SDK consists of several packages:

### sf-client

The core package for interacting with the Fixed-Rate Lending protocol.

```javascript
import { SecuredFinanceClient } from "@secured-finance/sf-client";
```

### sf-graph-client

Utilities for querying the Fixed-Rate Lending subgraph.

```javascript
import { GraphClient } from "@secured-finance/sf-graph-client";
```

### sf-core

Core components used across different Secured Finance projects.

```javascript
import { Currency, Token } from "@secured-finance/sf-core";
```

## Basic Usage

### Connecting to the Protocol

```javascript
import { SecuredFinanceClient } from "@secured-finance/sf-client";
import { createPublicClient, createWalletClient, http } from "viem";
import { filecoin } from "viem/chains";

// Connect to the protocol
async function connectToProtocol() {
  // Create viem clients
  const publicClient = createPublicClient({
    chain: filecoin,
    transport: http()
  });
  
  const walletClient = createWalletClient({
    chain: filecoin,
    transport: http()
  });
  
  // Create the Secured Finance client
  const client = new SecuredFinanceClient();
  await client.init(publicClient, walletClient);
  
  return client;
}
```

### Reading Protocol State

```javascript
import { Currency } from "@secured-finance/sf-core";

// Get supported currencies
async function getSupportedCurrencies(client) {
  const currencies = await client.getCurrencies();
  console.log("Supported currencies:", currencies);
  return currencies;
}

// Get lending markets
async function getLendingMarkets(client, currency) {
  const maturities = await client.getMaturities(currency);
  console.log("Available maturities:", maturities);
  
  const orderBookDetails = await client.getOrderBookDetailsPerCurrency(currency);
  console.log("Order book details:", orderBookDetails);
  
  return { maturities, orderBookDetails };
}

// Get order book
async function getOrderBook(client, currency, maturity) {
  const orderBookDetail = await client.getOrderBookDetail(currency, maturity);
  console.log("Order book detail:", orderBookDetail);
  
  const lendOrders = await client.getLendOrderBook(currency, maturity, 0, 10);
  console.log("Lend orders:", lendOrders);
  
  const borrowOrders = await client.getBorrowOrderBook(currency, maturity, 0, 10);
  console.log("Borrow orders:", borrowOrders);
  
  return { orderBookDetail, lendOrders, borrowOrders };
}

// Get user positions
async function getUserPositions(client, account) {
  const positions = await client.getPositions(account);
  console.log("User positions:", positions);
  return positions;
}
```

### Order Operations

```javascript
import { Currency } from "@secured-finance/sf-core";
import { OrderSide, WalletSource } from "@secured-finance/sf-client";

// Place a lend order
async function placeLendOrder(client, currency, maturity, amount, unitPrice) {
  const tx = await client.placeOrder(
    currency,
    maturity,
    OrderSide.LEND,
    amount,
    WalletSource.METAMASK,
    unitPrice
  );
  
  console.log("Lend order placed:", tx);
  return tx;
}

// Place a borrow order
async function placeBorrowOrder(client, currency, maturity, amount, unitPrice) {
  const tx = await client.placeOrder(
    currency,
    maturity,
    OrderSide.BORROW,
    amount,
    WalletSource.METAMASK,
    unitPrice
  );
  
  console.log("Borrow order placed:", tx);
  return tx;
}

// Cancel an order
async function cancelOrder(client, currency, maturity, orderId) {
  const tx = await client.cancelLendingOrder(currency, maturity, orderId);
  console.log("Order cancelled:", tx);
  return tx;
}
```

### Collateral Management

```javascript
// Deposit collateral
async function depositCollateral(client, currency, amount) {
  const tx = await client.depositCollateral(currency, amount);
  console.log("Collateral deposited:", tx);
  return tx;
}

// Get protocol deposit amount
async function getProtocolDepositAmount(client) {
  const depositAmount = await client.getProtocolDepositAmount();
  console.log("Protocol deposit amount:", depositAmount);
  return depositAmount;
}
```

### Position Management

```javascript
// Unwind a position
async function unwindPosition(client, currency, maturity) {
  const tx = await client.unwindPosition(currency, maturity);
  console.log("Position unwound:", tx);
  return tx;
}

// Get total present value
async function getTotalPresentValue(client) {
  const presentValue = await client.getTotalPresentValueInBaseCurrency();
  console.log("Total present value:", presentValue);
  return presentValue;
}
```

## Advanced Usage

### Using the Graph Client

```javascript
import { GraphClient } from "@secured-finance/sf-graph-client";
import { formatUnits } from "viem";

// Create a graph client for a specific network
const graphClient = new GraphClient({
  uri: "https://api.studio.thegraph.com/query/64582/sf-prd-arbitrum-sepolia/version/latest"
});

// Example: Fetch user positions with detailed market data
async function fetchUserPositions(userAddress) {
  const { user } = await graphClient.query({
    user: {
      __args: {
        id: userAddress.toLowerCase()
      },
      id: true,
      positions: {
        id: true,
        side: true,
        amount: true,
        presentValue: true,
        createdAt: true,
        updatedAt: true,
        market: {
          id: true,
          currency: {
            id: true,
            symbol: true,
            decimals: true
          },
          maturity: true
        }
      }
    }
  });

  if (!user || !user.positions || user.positions.length === 0) {
    console.log("No positions found for user:", userAddress);
    return [];
  }

  // Process and format the position data
  const formattedPositions = user.positions.map(position => {
    const { market, amount, presentValue, side, createdAt } = position;
    const { currency, maturity } = market;
    
    // Format amounts using proper decimals
    const formattedAmount = formatUnits(BigInt(amount), currency.decimals);
    const formattedPresentValue = formatUnits(BigInt(presentValue), currency.decimals);
    
    // Format maturity date
    const maturityDate = new Date(Number(maturity) * 1000).toLocaleDateString();
    
    return {
      id: position.id,
      currency: currency.symbol,
      maturityDate,
      side,
      amount: formattedAmount,
      presentValue: formattedPresentValue,
      createdAt: new Date(Number(createdAt) * 1000).toLocaleDateString()
    };
  });

  console.log("User positions:", formattedPositions);
  return formattedPositions;
}

// Example: Get market overview with order book depth
async function getMarketOverview(currencySymbol = "USDC") {
  // First query all markets for the specified currency
  const { currencies } = await graphClient.query({
    currencies: {
      __args: {
        where: {
          symbol: currencySymbol
        }
      },
      id: true,
      symbol: true,
      decimals: true,
      markets: {
        id: true,
        maturity: true,
        lastPrice: true,
        openingDate: true,
        isReady: true
      }
    }
  });

  if (!currencies || currencies.length === 0) {
    console.log(`No markets found for currency: ${currencySymbol}`);
    return [];
  }

  const currency = currencies[0];
  
  // For each market, get order book depth
  const marketsWithDepth = await Promise.all(
    currency.markets.map(async (market) => {
      // Get lend orders
      const { orders: lendOrders } = await graphClient.query({
        orders: {
          __args: {
            where: {
              market: market.id,
              side: "LEND",
              status_in: ["PENDING", "PARTIALLY_EXECUTED"]
            },
            orderBy: "price",
            orderDirection: "desc",
            first: 5
          },
          id: true,
          amount: true,
          price: true
        }
      });

      // Get borrow orders
      const { orders: borrowOrders } = await graphClient.query({
        orders: {
          __args: {
            where: {
              market: market.id,
              side: "BORROW",
              status_in: ["PENDING", "PARTIALLY_EXECUTED"]
            },
            orderBy: "price",
            orderDirection: "asc",
            first: 5
          },
          id: true,
          amount: true,
          price: true
        }
      });

      // Calculate total volume
      const lendVolume = lendOrders.reduce(
        (sum, order) => sum + BigInt(order.amount),
        0n
      );
      const borrowVolume = borrowOrders.reduce(
        (sum, order) => sum + BigInt(order.amount),
        0n
      );

      // Format maturity date
      const maturityDate = new Date(Number(market.maturity) * 1000);

      return {
        id: market.id,
        maturity: market.maturity,
        maturityDate: maturityDate.toLocaleDateString(),
        lastPrice: market.lastPrice ? formatUnits(BigInt(market.lastPrice), 4) : "N/A",
        lendOrders: lendOrders.length,
        borrowOrders: borrowOrders.length,
        lendVolume: formatUnits(lendVolume, currency.decimals),
        borrowVolume: formatUnits(borrowVolume, currency.decimals),
        isActive: market.isReady && Number(market.maturity) > Date.now() / 1000
      };
    })
  );

  // Sort by maturity date (ascending)
  marketsWithDepth.sort((a, b) => Number(a.maturity) - Number(b.maturity));
  
  console.log(`Market overview for ${currencySymbol}:`, marketsWithDepth);
  return marketsWithDepth;
}
```

### Price Calculations

```javascript
import { getUTCMonthYear } from "@secured-finance/sf-core";

// Convert unit price to APR
function unitPriceToAPR(unitPrice, maturity) {
  const now = Math.floor(Date.now() / 1000);
  const daysToMaturity = (maturity - now) / (60 * 60 * 24);
  
  // Convert unit price to APR
  const apr = ((10000 / unitPrice) - 1) * (365 / daysToMaturity) * 100;
  
  return apr;
}

// Format maturity date
function formatMaturity(maturity) {
  return getUTCMonthYear(maturity, true);
}

// Calculate order estimation
async function calculateOrderEstimation(client, currency, maturity, account, side, amount, unitPrice) {
  const estimation = await client.getOrderEstimation(
    currency,
    maturity,
    account,
    side,
    amount,
    unitPrice
  );
  
  console.log("Order estimation:", estimation);
  return estimation;
}
```

## Examples

### Creating a Lending Position

```javascript
import { SecuredFinanceClient, OrderSide, WalletSource } from "@secured-finance/sf-client";
import { Currency } from "@secured-finance/sf-core";
import { createPublicClient, createWalletClient, http } from "viem";
import { filecoin } from "viem/chains";

async function createLendingPosition() {
  // Connect to the protocol
  const publicClient = createPublicClient({
    chain: filecoin,
    transport: http()
  });
  
  const walletClient = createWalletClient({
    chain: filecoin,
    transport: http()
  });
  
  const client = new SecuredFinanceClient();
  await client.init(publicClient, walletClient);
  
  // Get the user's address
  const [address] = await walletClient.getAddresses();
  
  // Get supported currencies
  const currencies = await client.getCurrencies();
  const usdcCurrency = currencies.find(c => c.symbol === "USDC");
  
  if (!usdcCurrency) {
    throw new Error("USDC currency not found");
  }
  
  // Get available maturities
  const maturities = await client.getMaturities(usdcCurrency);
  
  if (maturities.length === 0) {
    throw new Error("No maturities available for USDC");
  }
  
  // Choose the nearest maturity
  const maturity = maturities[0];
  
  // Get the best lend unit price
  const bestLendUnitPrices = await client.getBestLendUnitPrices(usdcCurrency);
  const bestLendUnitPrice = bestLendUnitPrices.find(p => p.maturity === maturity);
  
  if (!bestLendUnitPrice) {
    throw new Error("No best lend unit price found for the selected maturity");
  }
  
  // Deposit collateral
  const collateralAmount = 1000n * 10n ** 6n; // 1000 USDC (assuming 6 decimals)
  await client.depositCollateral(usdcCurrency, collateralAmount);
  
  // Place a lend order
  const lendAmount = 500n * 10n ** 6n; // 500 USDC
  const unitPrice = bestLendUnitPrice.unitPrice;
  
  try {
    const tx = await client.placeOrder(
      usdcCurrency,
      maturity,
      OrderSide.LEND,
      lendAmount,
      WalletSource.METAMASK,
      unitPrice
    );
    
    console.log("Lend order placed successfully:", tx);
    
    // Get the user's positions
    const positions = await client.getPositions(address);
    console.log("User positions:", positions);
    
    return positions;
  } catch (error) {
    console.error("Error placing lend order:", error);
    throw error;
  }
}
```

### Monitoring Order Book and Placing Market Orders

```javascript
import { SecuredFinanceClient, OrderSide, WalletSource } from "@secured-finance/sf-client";
import { Currency } from "@secured-finance/sf-core";
import { createPublicClient, createWalletClient, http } from "viem";
import { filecoin } from "viem/chains";

async function monitorAndPlaceMarketOrder() {
  // Connect to the protocol
  const publicClient = createPublicClient({
    chain: filecoin,
    transport: http()
  });
  
  const walletClient = createWalletClient({
    chain: filecoin,
    transport: http()
  });
  
  const client = new SecuredFinanceClient();
  await client.init(publicClient, walletClient);
  
  // Get supported currencies
  const currencies = await client.getCurrencies();
  const usdcCurrency = currencies.find(c => c.symbol === "USDC");
  
  if (!usdcCurrency) {
    throw new Error("USDC currency not found");
  }
  
  // Get available maturities
  const maturities = await client.getMaturities(usdcCurrency);
  
  if (maturities.length === 0) {
    throw new Error("No maturities available for USDC");
  }
  
  // Choose the nearest maturity
  const maturity = maturities[0];
  
  // Monitor the order book
  const orderBookDetail = await client.getOrderBookDetail(usdcCurrency, maturity);
  console.log("Order book detail:", orderBookDetail);
  
  const lendOrders = await client.getLendOrderBook(usdcCurrency, maturity, 0, 10);
  console.log("Lend orders:", lendOrders);
  
  
  const borrowOrders = await client.getBorrowOrderBook(usdcCurrency, maturity, 0, 10);
  console.log("Borrow orders:", borrowOrders);
  
  // Check if there are any borrow orders
  if (borrowOrders.length === 0) {
    console.log("No borrow orders available");
    return null;
  }
  
  // Place a market order to lend (match against the best borrow order)
  const bestBorrowOrder = borrowOrders[0];
  const lendAmount = bestBorrowOrder.amount / 2n; // Lend half of the best borrow order amount
  
  // Deposit collateral
  await client.depositCollateral(usdcCurrency, lendAmount);
  
  // Place a market order (unitPrice = 0 for market orders)
  try {
    const tx = await client.placeOrder(
      usdcCurrency,
      maturity,
      OrderSide.LEND,
      lendAmount,
      WalletSource.METAMASK,
      0 // Market order
    );
    
    console.log("Market order placed successfully:", tx);
    return tx;
  } catch (error) {
    console.error("Error placing market order:", error);
    throw error;
  }
}
```

## FAQ

### How do I handle transaction errors?
The SDK throws descriptive error objects that contain information about the failure. Wrap your transactions in try-catch blocks to handle errors gracefully.

```javascript
try {
  await client.placeOrder(
    currency,
    maturity,
    OrderSide.LEND,
    amount,
    WalletSource.METAMASK,
    unitPrice
  );
} catch (error) {
  if (error.message.includes("InsufficientDepositAmount")) {
    console.error("Insufficient deposit amount. Deposit more collateral.");
  } else {
    console.error("Transaction failed:", error);
  }
}
```

### How do I convert between unit price and APR?
Use the following formula to convert unit price to APR:

```javascript
function unitPriceToAPR(unitPrice, maturity) {
  const now = Math.floor(Date.now() / 1000);
  const daysToMaturity = (maturity - now) / (60 * 60 * 24);
  
  // Convert unit price to APR
  const apr = ((10000 / unitPrice) - 1) * (365 / daysToMaturity) * 100;
  
  return apr;
}
```

### What networks does the SDK support?
The SDK supports all networks where the Fixed-Rate Lending protocol is deployed, including Ethereum, Arbitrum, and Filecoin.

## Related Resources
- [Fixed-Rate Lending Protocol Documentation](../../fixed-rate-lending/overview/README.md)
- [Fixed-Rate Lending Subgraph Documentation](../api-reference/fixed-rate-lending-subgraph/README.md)
- [GitHub Repository](https://github.com/Secured-Finance/sf-sdk)
- [NPM Package](https://www.npmjs.com/package/@secured-finance/sf-sdk)
