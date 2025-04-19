# 🔦 Core Mechanics

Secured Finance's stablecoin protocol introduces a variety of innovative features that enable users to efficiently mint, manage and utilise **USDFC**, our decentralized, Filecoin-backed stablecoin. Below are the key features:

## [**Mint & Borrow**](mint-to-borrow.md)

Mint USDFC by locking Filecoin (FIL) as collateral with a minimum collateralization ratio of 110%. This ensures capital efficiency while allowing users to extract liquidity from their FIL holdings.

## [**Liquidation with Stability Pool**](stability-pool-liquidations.md)

The Stability Pool secures the protocol by covering liquidations. Users who deposit USDFC into the pool can receive discounted FIL from liquidated positions.

## [**Redemption for Peg Mechanism**](redemption-mechanism.md)

USDFC maintains a 1:1 peg to the USD through a redemption mechanism, allowing users to exchange USDFC for FIL at its peg value, stabilizing its price.

## [**Recovery Mode**](../advanced-topics/recovery-mode.md)

If the system-wide collateral ratio drops below 150%, the protocol enters Recovery Mode, prioritizing liquidations and restricting new borrowing to restore stability.
