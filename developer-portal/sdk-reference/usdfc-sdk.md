---
description: Documentation for the USDFC SDK
---

# 👛 USDFC SDK

The USDFC SDK is a comprehensive toolkit for developers to integrate and interact with the USDFC stablecoin protocol.

## Overview

USDFC is a collateralized debt platform built on the Filecoin blockchain. Users can lock up FIL as collateral and issue USDFC stablecoin tokens. The USDFC SDK provides a programmatic interface to interact with the protocol, allowing developers to build applications that leverage USDFC functionality.

## How It Works

The USDFC SDK is built on top of ethers.js and provides a type-safe interface to interact with the USDFC smart contracts. It abstracts away the complexity of direct contract interactions and provides a more developer-friendly API.

## Installation

The USDFC SDK packages are hosted on GitHub Packages registry, not the public NPM registry. You'll need to configure your `.npmrc` file to access them:

```bash
# Add this to your .npmrc file
@secured-finance:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN

# Then install the individual packages
npm install @secured-finance/stablecoin-lib-ethers
npm install @secured-finance/stablecoin-lib-react
npm install @secured-finance/stablecoin-lib-base
```

For more details on setting up authentication for GitHub Packages, see the [GitHub documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry#authenticating-to-github-packages).


## Key Components

The USDFC SDK consists of several packages:

### lib-ethers

The core package for interacting with the USDFC protocol using ethers.js.

```javascript
import { EthersSfStablecoin } from "@secured-finance/stablecoin-lib-ethers";
```

### lib-react

React hooks and components for building USDFC-integrated web applications.

```javascript
import { useSfStablecoinStore } from "@secured-finance/stablecoin-lib-react";
```



## Basic Usage

### Connecting to the Protocol

```javascript
import { EthersSfStablecoin } from "@secured-finance/stablecoin-lib-ethers";
import { ethers } from "ethers";

// Connect to the protocol
async function connectToProtocol() {
  // Create an ethers provider
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  
  // Request account access
  await provider.send("eth_requestAccounts", []);
  
  // Get the signer
  const signer = provider.getSigner();
  
  // Connect to the USDFC protocol
  const usdfc = await EthersSfStablecoin.connect(signer);
  
  return usdfc;
}
```

### Reading Protocol State

```javascript
// Get a user's Trove
async function getUserTrove(usdfc, userAddress) {
  const trove = await usdfc.getTrove(userAddress);
  
  console.log("Collateral:", trove.collateral.toString());
  console.log("Debt:", trove.debt.toString());
  console.log("Collateral Ratio:", trove.collateralRatio.toString());
  console.log("Status:", trove.status);
  
  return trove;
}

// Get protocol price
async function getPrice(usdfc) {
  const price = await usdfc.getPrice();
  console.log("FIL/USD Price:", price.toString());
  return price;
}

// Get total protocol stats
async function getProtocolStats(usdfc) {
  const total = await usdfc.getTotal();
  console.log("Total Collateral:", total.collateral.toString());
  console.log("Total Debt:", total.debt.toString());
  return total;
}
```

### Creating and Managing Troves

```javascript
import { Decimal } from "@secured-finance/stablecoin-lib-base";

// Open a new Trove
async function openTrove(usdfc, collateralAmount, borrowAmount) {
  const tx = await usdfc.openTrove({
    collateral: Decimal.from(collateralAmount),
    borrowDebtToken: Decimal.from(borrowAmount)
  });
  
  console.log("Trove opened:", tx);
  return tx;
}

// Adjust an existing Trove
async function adjustTrove(usdfc, collateralChange, debtChange) {
  const tx = await usdfc.adjustTrove({
    collateralChange: Decimal.from(collateralChange),
    debtChange: Decimal.from(debtChange)
  });
  
  console.log("Trove adjusted:", tx);
  return tx;
}

// Close a Trove
async function closeTrove(usdfc) {
  const tx = await usdfc.closeTrove();
  console.log("Trove closed:", tx);
  return tx;
}
```

### Stability Pool Operations

```javascript
// Deposit to Stability Pool
async function depositToStabilityPool(usdfc, amount) {
  const tx = await usdfc.depositDebtTokenInStabilityPool(Decimal.from(amount));
  console.log("Deposited to Stability Pool:", tx);
  return tx;
}

// Withdraw from Stability Pool
async function withdrawFromStabilityPool(usdfc, amount) {
  const tx = await usdfc.withdrawDebtTokenFromStabilityPool(Decimal.from(amount));
  console.log("Withdrawn from Stability Pool:", tx);
  return tx;
}

// Claim rewards from Stability Pool
async function claimStabilityPoolRewards(usdfc) {
  const tx = await usdfc.withdrawGainsFromStabilityPool();
  console.log("Claimed rewards:", tx);
  return tx;
}
```

### Redemption Operations

```javascript
// Redeem USDFC for collateral
async function redeemUSDFC(usdfc, amount) {
  const tx = await usdfc.redeemDebtToken(Decimal.from(amount));
  console.log("Redeemed USDFC:", tx);
  return tx;
}
```

### Liquidation Operations

```javascript
// Liquidate Troves
async function liquidateTroves(usdfc, addresses) {
  const tx = await usdfc.liquidate(addresses);
  console.log("Liquidated Troves:", tx);
  return tx;
}

// Liquidate up to a specific number of Troves
async function liquidateUpTo(usdfc, maxTroves) {
  const tx = await usdfc.liquidateUpTo(maxTroves);
  console.log("Liquidated up to", maxTroves, "Troves:", tx);
  return tx;
}
```

## Advanced Usage

### React Integration

```javascript
import React, { useEffect, useState } from "react";
import { useSfStablecoinStore, useSfStablecoinSelector } from "@secured-finance/stablecoin-lib-react";
import { EthersSfStablecoin } from "@secured-finance/stablecoin-lib-ethers";
import { ethers } from "ethers";

function USDFCApp() {
  const [usdfc, setUsdfc] = useState(null);
  const store = useSfStablecoinStore();
  
  // Select data from the store
  const { trove, price } = useSfStablecoinSelector(store, state => ({
    trove: state.trove,
    price: state.price
  }));
  
  // Connect to the protocol
  useEffect(() => {
    async function connect() {
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      await provider.send("eth_requestAccounts", []);
      const signer = provider.getSigner();
      
      const usdfcInstance = await EthersSfStablecoin.connect(signer, {
        useStore: "blockPolled"
      });
      
      setUsdfc(usdfcInstance);
    }
    
    connect();
  }, []);
  
  // Render the app
  return (
    <div>
      <h1>USDFC App</h1>
      
      {trove && (
        <div>
          <h2>Your Trove</h2>
          <p>Collateral: {trove.collateral.toString()} FIL</p>
          <p>Debt: {trove.debt.toString()} USDFC</p>
          <p>Collateral Ratio: {trove.collateralRatio.toString()}%</p>
        </div>
      )}
      
      {price && (
        <div>
          <h2>Current Price</h2>
          <p>FIL/USD: ${price.toString()}</p>
        </div>
      )}
      
      {/* Add UI components for interacting with the protocol */}
    </div>
  );
}
```

## Examples

### Creating a Trove and Minting USDFC

```javascript
import { EthersSfStablecoin } from "@secured-finance/stablecoin-lib-ethers";
import { Decimal } from "@secured-finance/stablecoin-lib-base";
import { ethers } from "ethers";

async function mintUSDFC() {
  // Connect to the protocol
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  await provider.send("eth_requestAccounts", []);
  const signer = provider.getSigner();
  const usdfc = await EthersSfStablecoin.connect(signer);
  
  // Get the current price
  const price = await usdfc.getPrice();
  console.log("Current FIL/USD price:", price.toString());
  
  // Calculate a safe collateral ratio (e.g., 200%)
  const collateralAmount = Decimal.from(5); // 5 FIL
  const maxBorrowAmount = collateralAmount.mul(price).div(Decimal.from(2)); // 200% collateral ratio
  
  console.log("Depositing", collateralAmount.toString(), "FIL as collateral");
  console.log("Borrowing", maxBorrowAmount.toString(), "USDFC");
  
  // Open a Trove
  try {
    const tx = await usdfc.openTrove({
      collateral: collateralAmount,
      borrowDebtToken: maxBorrowAmount
    });
    
    console.log("Trove opened successfully:", tx);
    
    // Get the updated Trove
    const trove = await usdfc.getTrove();
    console.log("Your Trove:", trove);
    
    return trove;
  } catch (error) {
    console.error("Error opening Trove:", error);
    throw error;
  }
}
```

### Monitoring Liquidation Risk

```javascript
import { EthersSfStablecoin } from "@secured-finance/stablecoin-lib-ethers";
import { Decimal } from "@secured-finance/stablecoin-lib-base";
import { ethers } from "ethers";

async function monitorLiquidationRisk() {
  // Connect to the protocol
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  await provider.send("eth_requestAccounts", []);
  const signer = provider.getSigner();
  const usdfc = await EthersSfStablecoin.connect(signer);
  
  // Get the user's Trove
  const trove = await usdfc.getTrove();
  if (!trove.status === "open") {
    console.log("No open Trove found");
    return null;
  }
  
  // Get the current price
  const price = await usdfc.getPrice();
  
  // Calculate current collateral ratio
  const collateralRatio = trove.collateral.mul(price).div(trove.debt).mul(100);
  console.log("Current collateral ratio:", collateralRatio.toString(), "%");
  
  // Check if in danger of liquidation
  const minSafeRatio = Decimal.from(120); // 120% is the minimum safe ratio
  
  if (collateralRatio.lt(minSafeRatio)) {
    console.log("WARNING: Your Trove is at risk of liquidation!");
    
    // Calculate additional collateral needed to reach a safe ratio
    const targetRatio = Decimal.from(150); // Target 150% for safety
    const currentCollateralValue = trove.collateral.mul(price);
    const targetCollateralValue = trove.debt.mul(targetRatio).div(100);
    const additionalCollateralValue = targetCollateralValue.sub(currentCollateralValue);
    const additionalCollateral = additionalCollateralValue.div(price);
    
    console.log("Add at least", additionalCollateral.toString(), "FIL to reach a safe ratio of 150%");
    
    return {
      isAtRisk: true,
      currentRatio: collateralRatio,
      additionalCollateralNeeded: additionalCollateral
    };
  } else {
    console.log("Your Trove is currently safe from liquidation");
    return {
      isAtRisk: false,
      currentRatio: collateralRatio,
      additionalCollateralNeeded: Decimal.from(0)
    };
  }
}
```

## FAQ

### How do I handle transaction errors?
The SDK throws descriptive error objects that contain information about the failure. Wrap your transactions in try-catch blocks to handle errors gracefully.

```javascript
try {
  await usdfc.openTrove({
    collateral: Decimal.from(5),
    borrowDebtToken: Decimal.from(1000)
  });
} catch (error) {
  if (error.message.includes("CollateralRatioTooLow")) {
    console.error("The collateral ratio is too low. Add more collateral or borrow less.");
  } else {
    console.error("Transaction failed:", error);
  }
}
```

### How do I monitor protocol events?
Use the block-polled store to automatically update your application state when protocol events occur.

```javascript
const usdfc = await EthersSfStablecoin.connect(signer, {
  useStore: "blockPolled"
});

// The store will automatically update when new blocks are mined
usdfc.store.onTroveChanged = (trove) => {
  console.log("Trove updated:", trove);
};
```

### What networks does the SDK support?
The SDK supports the Filecoin network, which is the only network where the USDFC protocol is deployed. The USDFC protocol is not available on Ethereum or Arbitrum networks.

## Related Resources
- [USDFC Protocol Documentation](../../usdfc-stablecoin/overview.md)
- [GitHub Repository](https://github.com/Secured-Finance/stablecoin-sdk)
- [NPM Package](https://www.npmjs.com/package/@secured-finance/stablecoin-sdk)
