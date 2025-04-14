# Documentation Structure Mapping Checklist (v2)

This document maps the previous documentation structure (on `docs-optimize` before this PR) to the new structure implemented in this PR.

## Introduction

- `README.md` -> `README.md` (Root remains entry point)
- *New File* -> `introduction/overview.md` (Specific intro page)
- `about-secured-finance/mission-and-vision.md` -> `introduction/mission-and-vision.md`
- `about-secured-finance/roadmap-2025/README.md` -> `introduction/roadmap/README.md`
- `about-secured-finance/roadmap-2025/roadmap-2024.md` -> `introduction/roadmap/roadmap-2024.md`
- `about-secured-finance/roadmap-2025/roadmap-2023.md` -> `introduction/roadmap/roadmap-2023.md`

### DeFi Starter Guide

- *New Directory* -> `introduction/defi-starter-guide/`
- `resources/knowledge-base/README.md` -> (Removed, content integrated)
- `resources/knowledge-base/defi-vs-cefi.md` -> `introduction/defi-starter-guide/defi-vs-cefi.md`
- `resources/knowledge-base/apr-vs-apy.md` -> `introduction/defi-starter-guide/apr-vs-apy.md`
- `resources/knowledge-base/gas-cost.md` -> `introduction/defi-starter-guide/gas-cost.md`
- `resources/knowledge-base/dao.md` -> `introduction/defi-starter-guide/dao.md`
- *New File* -> `introduction/defi-starter-guide/wallet-setup-and-management.md`
- *New File* -> `introduction/defi-starter-guide/understanding-gas.md`
- *New File* -> `introduction/defi-starter-guide/interacting-with-dapps.md`

*(Note: `resources/knowledge-base/discount-factor.md` moved to Fixed-Rate Lending)*

---

## USDFC Stablecoin

- `usdfc-stablecoin/overview.md` -> `usdfc-stablecoin/overview.md`
- `usdfc-stablecoin/getting-started.md` -> `usdfc-stablecoin/getting-started/README.md`
- *New File* -> `usdfc-stablecoin/getting-started/creating-your-first-trove.md`
- *New File* -> `usdfc-stablecoin/getting-started/minting-usdfc-step-by-step.md`
- *New File* -> `usdfc-stablecoin/getting-started/managing-collateral-effectively.md`
- *New File* -> `usdfc-stablecoin/getting-started/monitoring-your-position.md`
- (Existing content to be refactored) -> `usdfc-stablecoin/getting-started/using-the-stability-pool.md`
- (Existing content to be refactored) -> `usdfc-stablecoin/getting-started/redeeming-usdfc.md`
- `usdfc-stablecoin/core-mechanics/README.md` -> `usdfc-stablecoin/core-mechanics/README.md`
- `usdfc-stablecoin/advanced-topics/trove-management.md` -> `usdfc-stablecoin/core-mechanics/the-trove-system.md` (Concept Integration)
- `usdfc-stablecoin/core-mechanics/stability-pool-liquidations.md` -> `usdfc-stablecoin/core-mechanics/stability-pool.md` (Concept Integration)
- `usdfc-stablecoin/core-mechanics/redemption-mechanism.md` -> `usdfc-stablecoin/core-mechanics/redemption.md` (Concept Integration)
- `usdfc-stablecoin/core-mechanics/mint-to-borrow.md` -> `usdfc-stablecoin/core-mechanics/mint-and-borrow.md` (Renamed for consistency)
- `usdfc-stablecoin/core-mechanics/protocol-fees.md` -> `usdfc-stablecoin/core-mechanics/protocol-fees.md`
- `usdfc-stablecoin/advanced-topics/README.md` -> `usdfc-stablecoin/advanced-topics/README.md`
- `usdfc-stablecoin/advanced-topics/recovery-mode.md` -> `usdfc-stablecoin/advanced-topics/recovery-mode.md`
- `usdfc-stablecoin/advanced-topics/community-resources.md` -> `developer-portal/architecture.md` (Moved)
- `usdfc-stablecoin/deployed-contracts.md` -> `usdfc-stablecoin/deployed-contracts.md`
- `usdfc-stablecoin/faqs.md` -> `usdfc-stablecoin/faqs.md`

---

## Fixed-Rate Lending

- `fixed-rate-lending/overview/README.md` -> `fixed-rate-lending/overview/README.md`
- `fixed-rate-lending/overview/white-paper.md` -> `fixed-rate-lending/overview/white-paper.md`
- `fixed-rate-lending/overview/concept-paper.md` -> `fixed-rate-lending/overview/concept-paper.md`
- `fixed-rate-lending/getting-started/README.md` -> `fixed-rate-lending/getting-started/README.md`
- `fixed-rate-lending/getting-started/platform-guide/*` -> `fixed-rate-lending/getting-started/platform-guide/*` (Remains nested)
- *New File* -> `fixed-rate-lending/getting-started/lending-assets.md`
- *New File* -> `fixed-rate-lending/getting-started/borrowing-assets.md`
- *New File* -> `fixed-rate-lending/getting-started/managing-positions.md`
- `fixed-rate-lending/protocol-features/README.md` -> `fixed-rate-lending/core-mechanics/README.md`
- `fixed-rate-lending/protocol-features/on-chain-orderbook-system.md` -> `fixed-rate-lending/core-mechanics/order-book-system.md` (Concept Integration)
- `fixed-rate-lending/protocol-features/zero-coupon-standard.md` -> `fixed-rate-lending/core-mechanics/zero-coupon-bonds.md` (Concept Integration)
- `fixed-rate-lending/protocol-features/fixed-maturity-standard.md` -> `fixed-rate-lending/core-mechanics/fixed-maturity.md` (Concept Integration)
- `fixed-rate-lending/advanced-topics/zero-coupon-bond-tokenization.md` -> `fixed-rate-lending/core-mechanics/tokenization.md` (Concept Integration)
- `fixed-rate-lending/protocol-features/liquidation/*` -> `fixed-rate-lending/core-mechanics/liquidation-process/*` (Concept Integration)
- `fixed-rate-lending/protocol-features/protocol-fees.md` -> `fixed-rate-lending/core-mechanics/protocol-fees.md`
- `fixed-rate-lending/advanced-topics/README.md` -> `fixed-rate-lending/advanced-topics/README.md`
- `fixed-rate-lending/advanced-topics/zc-bond-price-to-apr.md` -> `fixed-rate-lending/advanced-topics/zc-bond-price-to-apr.md`
- `resources/knowledge-base/discount-factor.md` -> `fixed-rate-lending/advanced-topics/discount-factor.md` (Moved from Knowledge Base)
- `fixed-rate-lending/advanced-topics/zc-bond-collateral/*` -> `fixed-rate-lending/advanced-topics/zc-bond-collateral/*`
- `fixed-rate-lending/advanced-topics/market-dynamics/*` -> `fixed-rate-lending/advanced-topics/market-dynamics/*`
- `fixed-rate-lending/advanced-topics/safety-measures/*` -> `fixed-rate-lending/advanced-topics/safety-measures/*`
- `fixed-rate-lending/advanced-topics/on-chain-orderbook-deep-dive/*` -> `developer-portal/orderbook-deep-dive/*` (Moved to Developer Portal)
- `fixed-rate-lending/deployed-contracts.md` -> `fixed-rate-lending/deployed-contracts.md`
- `fixed-rate-lending/faqs.md` -> `fixed-rate-lending/faqs.md`

---

## Developer Portal

- `developer-resources/developer-introduction.md` -> `developer-portal/introduction.md`
- `developer-resources/api-documentation/*` -> `developer-portal/api-reference/fixed-rate-lending-subgraph/*`
- *New File* -> `developer-portal/api-reference/README.md`
- *New File* -> `developer-portal/api-reference/usdfc-subgraph.md`
- `sdk-integration.md` -> `developer-portal/sdk-reference/README.md`
- *New File* -> `developer-portal/sdk-reference/usdfc-sdk.md`
- *New File* -> `developer-portal/sdk-reference/fixed-rate-lending-sdk.md`
- `fixed-rate-lending/advanced-topics/on-chain-orderbook-deep-dive/*` -> `developer-portal/orderbook-deep-dive/*` (Moved from Fixed-Rate Lending)
- `usdfc-stablecoin/advanced-topics/community-resources.md` -> `developer-portal/architecture.md` (Moved from USDFC)
- `bug-bounty-program.md` -> `developer-portal/bug-bounty.md`

---

## Community

- *New Directory* -> `community/`
- `community-and-support/governance.md` -> `community/governance.md`
- `community-and-support/tokenomics/*` -> `community/tokenomics/*`
- `community-and-support/contact-us.md` -> `community/support-and-contacts.md`

---

## Resources

- `resources/media-kit/*` -> `resources/media-kit/*`
- `legal/*` -> `resources/legal/*`

---
