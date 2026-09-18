---
description: The components of the USDFC protocol and how they fit together
---

# 🏗️ System Overview

USDFC is a decentralized protocol that mints a USD-pegged stablecoin against FIL collateral. Its stability rests on a small set of interlocking mechanisms — each has its own page in this section; this one shows how they connect.

## The components

1. **[Troves](the-trove-system.md)** — individual positions where users lock FIL and mint USDFC, each subject to a 110% minimum collateral ratio (150% to open during Recovery Mode).
2. **[Stability Pool](stability-pool.md)** — a reserve of USDFC that repays the debt of liquidated Troves; depositors receive the seized FIL.
3. **[Liquidation](liquidation.md)** — lets anyone close a Trove that falls below the minimum ratio, resolving its debt through the Stability Pool or, if the pool falls short, redistribution.
4. **[Redemption](redemption.md)** — lets any holder exchange USDFC for $1 worth of FIL (minus a redemption fee) from the lowest-ratio Troves, anchoring the peg from below.
5. **[Price Oracle](price-oracle.md)** — supplies the FIL/USD price that all ratio checks depend on.
6. **[Recovery Mode](recovery-mode.md)** — stricter rules that activate when the system-wide collateral ratio falls below 150%.

The causal chain: the oracle prices the collateral → ratios determine which Troves are safe → liquidation and the Stability Pool remove unsafe debt → redemption supports the peg from below → Recovery Mode hardens all of it when the whole system is stressed.

<!-- Architecture diagrams (Normal Mode / Recovery Mode, .gitbook/assets/image (5) (1).png and image (1) (1) (1) (1).png) temporarily removed: the artwork carries pre-launch notes that contradict the text. Restore the "Architecture" section from git history once corrected artwork is ready. -->

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
