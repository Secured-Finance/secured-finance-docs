---
description: The components of the USDFC protocol and how they fit together
---

# 🏗️ System Overview

USDFC is a decentralized protocol that mints a USD-pegged stablecoin against FIL collateral. Its stability rests on a small set of interlocking mechanisms — each has its own page in this section; this one shows how they connect.

## The components

1. **[Troves](the-trove-system.md)** — individual positions where users lock FIL and mint USDFC, each subject to a 110% minimum collateral ratio (150% to open during Recovery Mode).
2. **[Stability Pool](stability-pool.md)** — a reserve of USDFC that repays the debt of liquidated Troves; depositors receive the seized FIL.
3. **[Liquidation](liquidation.md)** — lets anyone close a Trove that falls below the minimum ratio, resolving its debt through the Stability Pool or redistribution to other Troves.
4. **[Redemption](redemption.md)** — lets any holder exchange USDFC for $1 worth of FIL (minus a redemption fee) from the lowest-ratio Troves, anchoring the peg from below.
5. **[Price Oracle](price-oracle.md)** — supplies the FIL/USD price that all ratio checks depend on.
6. **[Recovery Mode](recovery-mode.md)** — stricter rules that activate when the system-wide collateral ratio falls below 150%.

The causal chain: the oracle prices the collateral → ratios determine which Troves are safe → liquidation and the Stability Pool remove unsafe debt → redemption supports the peg from below → Recovery Mode hardens all of it when the whole system is stressed.

## Architecture

### Normal Mode

<figure><img src="../../.gitbook/assets/usdfc-architecture-normal-mode.png" alt="Flow diagram of Normal Mode: a user connects a wallet, deposits FIL into a Trove at a minimum 110% collateral ratio with 0% interest, and mints USDFC; 20 USDFC is set aside as the Liquidation Reserve, which is not repaid on close; the one-off minting fee (0.5% to 5% in USDFC) and redemption fees (in FIL) go to the Fee Reserve for future distribution; USDFC can be deposited into the Stability Pool; a Trove under 110% is liquidated with its FIL going to Stability Pool depositors and 0.5% plus 20 USDFC to the liquidator; a redeemer exchanges USDFC for FIL at face value, before the redemption fee, from a Trove above 110%; minimum net debt is 200 USDFC excluding the reserve; the liquidation shown assumes sufficient Stability Pool deposits, otherwise remaining debt and collateral are redistributed to other Troves"><figcaption><p>USDFC protocol architecture in Normal Mode</p></figcaption></figure>

### Recovery Mode

<figure><img src="../../.gitbook/assets/usdfc-architecture-recovery-mode.png" alt="Flow diagram of Recovery Mode, triggered when TCR is below 150%: Troves at or below 100% are liquidated by redistributing their debt and collateral to other Troves; Troves between 100% and 110% are offset against the Stability Pool with any remainder redistributed; Troves between 110% and the TCR (for example a Trove at 140% when the TCR is 148%) are liquidated only if the Stability Pool can cover the entire debt, with liquidated collateral capped at 110% of debt, the Trove closed, and the remaining collateral (worth 30% of debt in the example) sent to CollSurplusPool for the owner to claim; new Troves need a ratio of at least 150%, and it is not possible to withdraw collateral, close a Trove, or increase debt unless the resulting ratio is at least 150% and does not decrease; the 0.5% liquidator share is not shown"><figcaption><p>USDFC protocol architecture in Recovery Mode</p></figcaption></figure>

## Key parameters

| Parameter | Description | Value |
| --- | --- | --- |
| Minimum Collateral Ratio (MCR) | Per-Trove ratio below which liquidation is possible | 110% |
| Critical Collateral Ratio (CCR) | System-wide ratio that triggers Recovery Mode | 150% |
| Minimum net debt | Borrowed amount plus borrowing fee, excluding the 20 USDFC reserve (the app enforces this as a 200 USDFC minimum borrow) | 200 USDFC |
| Liquidation Reserve | Added to each Trove's debt to cover liquidation gas; not repaid by you when you close | 20 USDFC |
| Borrowing fee | One-time, (Base Rate + 0.5%), capped at 5% | 0.5% – 5% |
| Redemption fee | (Base Rate + 0.5%) of the FIL drawn, paid in FIL; not capped at 5% | 0.5% minimum |
| Interest | Ongoing charge on debt | None |

The **Base Rate** is a single system-wide variable that rises with redemption volume and decays with a 12-hour half-life — the full mechanics are in [Mint & Borrow](mint-and-borrow.md#base-rate-explanation).
