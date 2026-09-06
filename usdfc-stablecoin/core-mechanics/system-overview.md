---
description: The components of the USDFC protocol and how they fit together
---

# 🏗️ System Overview

USDFC is a decentralized protocol that mints a USD-pegged stablecoin against FIL collateral. Its stability rests on a small set of interlocking mechanisms — each has its own page in this section; this one shows how they connect.

## The components

1. **[Troves](the-trove-system.md)** — individual positions where users lock FIL and mint USDFC, each keeping a collateral ratio above 110%.
2. **[Stability Pool](stability-pool.md)** — a reserve of USDFC that repays the debt of liquidated Troves; depositors receive the seized FIL.
3. **[Liquidation](liquidation.md)** — resolves any Trove that falls below the minimum ratio, keeping the system solvent.
4. **[Redemption](redemption.md)** — lets any holder exchange USDFC for $1 of FIL from the lowest-ratio Troves, anchoring the peg from below.
5. **[Price Oracle](price-oracle.md)** — supplies the FIL/USD price that all ratio checks depend on.
6. **[Recovery Mode](recovery-mode.md)** — stricter rules that activate when the system-wide collateral ratio falls below 150%.

The causal chain: the oracle prices the collateral → ratios determine which Troves are safe → liquidation and the Stability Pool remove unsafe debt → redemption ties the token's floor to $1 → Recovery Mode hardens all of it when the whole system is stressed.

## Architecture

### Normal Mode

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt="Normal Mode Architecture"><figcaption><p>USDFC protocol architecture in Normal Mode</p></figcaption></figure>

### Recovery Mode

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt="Recovery Mode Architecture"><figcaption><p>USDFC protocol architecture in Recovery Mode</p></figcaption></figure>

## Key parameters

| Parameter | Description | Value |
| --- | --- | --- |
| Minimum Collateral Ratio (MCR) | Per-Trove ratio below which liquidation is possible | 110% |
| Critical Collateral Ratio (CCR) | System-wide ratio that triggers Recovery Mode | 150% |
| Minimum borrow amount | Smallest amount a Trove can borrow (total debt is higher: this plus fee and reserve) | 200 USDFC |
| Liquidation Reserve | Set aside per Trove for liquidation gas; refunded on close | 20 USDFC |
| Borrowing fee | One-time, (Base Rate + 0.5%), capped at 5% | 0.5% – 5% |
| Redemption fee | (Base Rate + 0.5%) of the redeemed amount, paid in FIL | 0.5% minimum |
| Interest | Ongoing charge on debt | None |

The **Base Rate** is a single system-wide variable that rises with redemption volume and decays with a 12-hour half-life — the full mechanics are in [Mint & Borrow](mint-and-borrow.md#base-rate-explanation).
