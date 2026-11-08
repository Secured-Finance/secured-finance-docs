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

{% code collapsedlinecount="10" %}
```bash
# Add this to your .npmrc file
@secured-finance:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=YOUR_GITHUB_TOKEN

# Then install the individual packages
npm install @secured-finance/stablecoin-lib-ethers
npm install @secured-finance/stablecoin-lib-react
npm install @secured-finance/stablecoin-lib-base
```
{% endcode %}

For more details on setting up authentication for GitHub Packages, see the [GitHub documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry#authenticating-to-github-packages).

## Key Components

The USDFC SDK consists of several packages:

### lib-ethers

The core package for interacting with the USDFC protocol using ethers.js.

{% code collapsedlinecount="10" %}
```javascript
import { EthersSfStablecoin } from "@secured-finance/stablecoin-lib-ethers";
```
{% endcode %}

### lib-react

React hooks and components for building USDFC-integrated web applications.

{% code collapsedlinecount="10" %}
```javascript
import { useSfStablecoinStore } from "@secured-finance/stablecoin-lib-react";
```
{% endcode %}

## Basic Usage

### Connecting to the Protocol

{% code collapsedlinecount="10" %}
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
{% endcode %}

### Reading Protocol State

{% code collapsedlinecount="10" %}
```javascript
// Get a user's Trove
async function getUserTrove(usdfc, userAddress) {
  const trove = await usdfc.getTrove(userAddress);
  
  console.log("Collateral:", trove.collateral.toString());
  console.log("Debt:", trove.debt.toString());
  // Display only: a ratio alone does not establish current liquidation risk.
  const price = await usdfc.getPrice();
  if (trove.status === "open" && trove.debt.gt(0) && price.gt(0)) {
    console.log("Collateral Ratio:", trove.collateralRatio(price).mul(100).toString(), "%");
  }
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
{% endcode %}

### Creating and Managing Troves

Creation takes `depositCollateral` and `borrowDebtToken`. Adjustments use `depositCollateral` or `withdrawCollateral`, and `borrowDebtToken` or `repayDebtToken`. Specify at least one change; do not combine both collateral directions or both debt directions in one adjustment. These are [SDK parameter names](https://github.com/Secured-Finance/stablecoin-sdk/blob/030746129c886eedea132b40791fea9d16ba3ca2/packages/lib-base/src/Trove.ts#L13-L174), not signed `collateralChange`/`debtChange` fields.

{% code collapsedlinecount="10" %}
```javascript
import { Decimal } from "@secured-finance/stablecoin-lib-base";

// Open a new Trove
async function openTrove(usdfc, collateralAmount, borrowAmount) {
  const tx = await usdfc.openTrove({
    depositCollateral: Decimal.from(collateralAmount),
    borrowDebtToken: Decimal.from(borrowAmount)
  });
  
  console.log("Trove opened:", tx);
  return tx;
}

// Adjust an existing Trove using the directional SDK parameters.
// Example adjustment: { depositCollateral: "5", repayDebtToken: "100" }
async function adjustTrove(usdfc, adjustment) {
  const tx = await usdfc.adjustTrove(adjustment);
  
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
{% endcode %}

### Stability Pool Operations

{% code collapsedlinecount="10" %}
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
{% endcode %}

### Redemption Operations

{% code collapsedlinecount="10" %}
```javascript
// Redeem USDFC for collateral
async function redeemUSDFC(usdfc, amount) {
  const tx = await usdfc.redeemDebtToken(Decimal.from(amount));
  console.log("Redeemed USDFC:", tx);
  return tx;
}
```
{% endcode %}

### Liquidation Operations

{% code collapsedlinecount="10" %}
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
{% endcode %}

## Advanced Usage

### React Integration

`collateralRatio(price)` is a method; multiply its result by 100 only for percentage display. A displayed price or ratio may be stale and is not a liquidation-risk assessment. Use the source/freshness and same-block checks in [Monitoring Liquidation Risk](usdfc-sdk.md#monitoring-liquidation-risk) for risk monitoring. Pass an SDK instance connected with useStore set to "blockPolled" to USDFCApp below. SfStablecoinStoreProvider starts the store, waits for its first load and stops it on unmount; do not start that same store separately.

{% code collapsedlinecount="10" %}
```javascript
import React from "react";
import {
  SfStablecoinStoreProvider,
  useSfStablecoinSelector
} from "@secured-finance/stablecoin-lib-react";

function TroveDetails() {
  // The selector reads the store supplied by the surrounding provider.
  const { trove, price, priceSource, isPriceStale } =
    useSfStablecoinSelector(state => ({
      trove: state.trove,
      price: state.price,
      priceSource: state.priceSource,
      isPriceStale: state.isPriceStale
    }));

  return (
    <div>
      <h2>Your Trove</h2>
      <p>Status: {trove.status}</p>
      <p>Collateral: {trove.collateral.toString()} FIL</p>
      <p>Debt: {trove.debt.toString()} USDFC</p>
      {trove.status === "open" && trove.debt.gt(0) &&
        price.gt(0) && isPriceStale === false && (
          <p>Collateral Ratio: {trove.collateralRatio(price).mul(100).toString()}%</p>
        )}
      <p>Reported FIL/USD: {price.toString()}</p>
      <p>Oracle source: {priceSource}</p>
      {isPriceStale && <p>Stored oracle price is stale.</p>}
      <p>Display only. These values do not establish liquidation eligibility.</p>
    </div>
  );
}

// Connect once in your host application's wallet flow:
// const usdfc = await EthersSfStablecoin.connect(signer, {
//   useStore: "blockPolled"
// });
export function USDFCApp({ usdfc }) {
  if (!usdfc) return <p>Connect a wallet to load your Trove.</p>;

  return (
    <SfStablecoinStoreProvider
      store={usdfc.store}
      loader={<p>Loading protocol state...</p>}
    >
      <TroveDetails />
    </SfStablecoinStoreProvider>
  );
}
```
{% endcode %}

## Examples

### Creating a Trove and Minting USDFC

Choose the collateral and requested borrow amount explicitly. The opening ratio uses **total debt**, including the borrowing fee and Liquidation Reserve, not just the USDFC received in the wallet. With reserve 20 USDFC and fee rate 0.5%, borrowing 200 USDFC creates 221 USDFC of total debt; collateral worth $442 gives a 200% ratio at that price. A 200% target is a buffer, not a safety guarantee.

This read-only preview uses the current fee rate and [`Trove.create()`](https://github.com/Secured-Finance/stablecoin-sdk/blob/030746129c886eedea132b40791fea9d16ba3ca2/packages/lib-base/src/Trove.ts#L628-L676) to include the fee and reserve. It also checks the SDK's minimum **net debt** (borrowing plus fee, excluding the reserve). Confirm that the SDK reserve and minimum-debt configuration match the deployment; the documented Filecoin values are 20 and 200 USDFC respectively.

{% code collapsedlinecount="10" %}
```javascript
import {
  Decimal, Trove, LIQUIDATION_RESERVE, MINIMUM_NET_DEBT
} from "@secured-finance/stablecoin-lib-base";

// Read-only arithmetic preview, not a transaction or an eligibility check.
async function previewOpeningTrove(usdfc, provider, collateralInput, borrowInput) {
  const blockTag = await provider.getBlockNumber();
  const overrides = { blockTag };
  const params = {
    depositCollateral: Decimal.from(collateralInput),
    borrowDebtToken: Decimal.from(borrowInput)
  };
  if (!params.depositCollateral.gt(0) || !params.borrowDebtToken.gt(0)) {
    throw new Error("Collateral and requested borrowing must be positive");
  }
  const [oracle, fees] = await Promise.all([
    usdfc.getPriceWithSource(overrides),
    usdfc.getFees(overrides)
  ]);
  if (oracle.source !== "primaryOracle" || oracle.isStale !== false ||
      !oracle.price.gt(0)) {
    throw new Error("Opening a Trove requires a current primary-oracle price");
  }

  // getFees() accounts for Recovery Mode at the same block.
  const borrowingRate = fees.borrowingRate();
  const quotedTrove = Trove.create(params, borrowingRate);
  if (quotedTrove.netDebt.lt(MINIMUM_NET_DEBT)) {
    throw new Error("Borrowing plus its fee is below the minimum net debt");
  }
  return {
    blockTag, params, borrowingRate,
    borrowingFee: quotedTrove.netDebt.sub(params.borrowDebtToken),
    liquidationReserve: LIQUIDATION_RESERVE,
    totalDebt: quotedTrove.debt,
    collateralRatioPercent: quotedTrove.collateralRatio(oracle.price).mul(100)
  };
}
```
{% endcode %}

The returned amounts are SDK `Decimal` values; use `.toString()` for display. The preview does not send a transaction and does not check every opening restriction, wallet balance or gas cost. Before calling `openTrove`, review the resulting ICR, system TCR, mode restrictions and maximum acceptable borrowing fee, and simulate the transaction against current state. Price, fees and mode can change after the preview. See the [opening requirements](../../usdfc-stablecoin/core-mechanics/recovery-mode.md#what-changes) and [oracle requirements](../../usdfc-stablecoin/core-mechanics/price-oracle.md#which-actions-remain-available).

### Monitoring Liquidation Risk

This read-only example implements the [complete liquidation rules](../../usdfc-stablecoin/core-mechanics/recovery-mode.md#liquidation-behavior-in-recovery-mode) rather than using a single ratio threshold.

The read-only example below uses one block for the Trove (including pending redistribution), total system collateral and debt, oracle state, pool balance and Trove count. It returns `unknown` on missing data, stale/unknown oracle state or read failures. It does not send transactions or classify any position as "safe."

**API baseline:** this example uses `getPriceWithSource()` from [SDK source commit 0307461](https://github.com/Secured-Finance/stablecoin-sdk/blob/030746129c886eedea132b40791fea9d16ba3ca2/packages/lib-ethers/src/ReadableEthers.ts#L243-L325). The oracle-source API is available in @secured-finance/stablecoin-lib-ethers v1.3.0, released on 30 October 2026. Pin that version when reproducing this example; older builds must be upgraded or use an equivalent verified contract reader. BigInt requires an ES2020-compatible runtime.

{% code collapsedlinecount="10" %}
```javascript
// Read-only snapshot monitor. Requires a provider and an already connected SDK.
// Requires an SDK build with getPriceWithSource() and an ES2020 BigInt runtime.
function toWad(value) {
  const text = value?.toString();
  if (!text || !/^\d+(\.\d{1,18})?$/.test(text)) {
    throw new Error("Missing or invalid 18-decimal value");
  }
  const [whole, fraction = ""] = text.split(".");
  return BigInt(whole) * 10n ** 18n + BigInt(fraction.padEnd(18, "0"));
}

async function monitorLiquidationRisk(usdfc, provider, userAddress) {
  try {
    if (!userAddress || typeof usdfc.getPriceWithSource !== "function") {
      throw new Error("Address and an SDK with oracle-source support are required");
    }
    const blockTag = await provider.getBlockNumber();
    const overrides = { blockTag };
    const trove = await usdfc.getTrove(userAddress, overrides);
    if (!trove || typeof trove.status !== "string") {
      throw new Error("Missing Trove status");
    }
    if (trove.status !== "open") {
      return { status: "no-open-trove", blockTag };
    }

    const [oracle, total, pool, numberOfTroves] = await Promise.all([
      usdfc.getPriceWithSource(overrides),
      usdfc.getTotal(overrides),
      usdfc.getDebtTokenInStabilityPool(overrides),
      usdfc.getNumberOfTroves(overrides)
    ]);
    const knownSources = ["primaryOracle", "fallbackOracle", "lastGoodPrice"];
    if (!knownSources.includes(oracle?.source) || oracle.isStale !== false) {
      throw new Error("Oracle source or freshness is unusable or unknown");
    }
    const price = toWad(oracle.price);
    const debt = toWad(trove.debt);
    const collateral = toWad(trove.collateral);
    const totalDebt = toWad(total?.debt);
    const totalCollateral = toWad(total?.collateral);
    const poolDebt = toWad(pool);
    if (price === 0n || debt === 0n || totalDebt === 0n ||
        !Number.isInteger(numberOfTroves) || numberOfTroves < 1) {
      throw new Error("Missing or inconsistent protocol state");
    }

    // Match contract integer arithmetic: collateral * price / debt.
    // Ratios are scaled by 1e18, so 110% is 1.1e18.
    const ONE = 10n ** 18n;
    const MCR = 11n * ONE / 10n;
    const CCR = 15n * ONE / 10n;
    const icr = collateral * price / debt;
    const tcr = totalCollateral * price / totalDebt;
    const recoveryMode = tcr < CCR;
    let meetsLiquidationRule = false;
    let branch = "no-liquidation-branch";

    if (!recoveryMode && icr < MCR) {
      meetsLiquidationRule = true;
      branch = "normal-mode";
    } else if (recoveryMode && icr <= ONE) {
      meetsLiquidationRule = true;
      branch = "redistribution-only";
    } else if (recoveryMode && icr < MCR) {
      meetsLiquidationRule = true;
      branch = "offset-and-or-redistribution";
    } else if (recoveryMode && icr < tcr && poolDebt >= debt) {
      meetsLiquidationRule = true;
      branch = "capped-full-offset";
    }

    // The protocol does not close the last remaining Trove.
    const eligibleAtSnapshot = numberOfTroves > 1 && meetsLiquidationRule;
    return {
      status: eligibleAtSnapshot ? "eligible-at-snapshot" : "not-eligible-at-snapshot",
      blockTag, recoveryMode, branch, oracleSource: oracle.source,
      icrWad: icr.toString(), tcrWad: tcr.toString(),
      warning: "A snapshot is not a safety guarantee or a transaction simulation."
    };
  } catch (error) {
    return { status: "unknown", reason: String(error) };
  }
}
```
{% endcode %}

`icrWad` and `tcrWad` use 18-decimal ratio units: `1100000000000000000` means 110%. Preserve integer arithmetic for comparisons and format only for display. Call this function with an already-connected SDK, its provider and the address to inspect. Re-run it as new blocks arrive.

This is a single-Trove snapshot assessment, not a transaction-success promise or a batch-liquidation simulator. Other liquidations can change TCR and Stability Pool coverage before execution; price changes and redistribution can change the Trove. Re-simulate a proposed transaction against current state. Oracle fallback does not by itself block liquidation, but [risk-increasing borrower actions require a primary price](../../usdfc-stablecoin/core-mechanics/price-oracle.md).

## FAQ

### How do I handle transaction errors?

The SDK throws descriptive error objects that contain information about the failure. Wrap your transactions in try-catch blocks to handle errors gracefully.

{% code collapsedlinecount="10" %}
```javascript
try {
  await usdfc.openTrove({
    depositCollateral: Decimal.from(5),
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
{% endcode %}

### How do I monitor protocol events?

Use the block-polled store to observe changes in protocol state. Register a listener with subscribe(), start the store, and clean up both when finished. This polls state on new blocks; it is not a subscription to every raw contract event. In React, SfStablecoinStoreProvider manages the store lifecycle instead.

{% code collapsedlinecount="10" %}
```javascript
import { EthersSfStablecoin } from "@secured-finance/stablecoin-lib-ethers";

// Standalone usage, without SfStablecoinStoreProvider.
// signer must already be connected to the intended wallet and network.
async function watchTrove(signer) {
  const usdfc = await EthersSfStablecoin.connect(signer, {
    useStore: "blockPolled"
  });
  const store = usdfc.store;

  store.onLoaded = () => {
    console.log("Initial Trove:", store.state.trove);
  };
  const unsubscribe = store.subscribe(({ newState, stateChange }) => {
    if (stateChange.trove !== undefined) {
      console.log("Trove updated:", newState.trove);
    }
  });
  const stop = store.start();

  // Call this cleanup function when monitoring is no longer needed.
  return () => {
    unsubscribe();
    store.onLoaded = undefined;
    stop();
  };
}

// const stopWatching = await watchTrove(signer);
// Later, when leaving the view or disconnecting:
// stopWatching();
```
{% endcode %}

### What networks does the SDK support?

The SDK supports the Filecoin network, which is the only network where the USDFC protocol is deployed. The USDFC protocol is not available on Ethereum or Arbitrum networks.

## Related Resources

* [USDFC Protocol Documentation](../../usdfc-stablecoin/overview.md)
* [GitHub Repository](https://github.com/Secured-Finance/stablecoin-sdk)
* [GitHub Packages installation and registry setup](usdfc-sdk.md#installation)
