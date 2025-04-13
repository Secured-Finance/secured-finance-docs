# Documentation Structure Mapping Checklist

This document maps the old documentation structure to the new structure implemented in this PR.

## About Secured Finance

- [x] `README.md` → `about/README.md`
- [x] `top/our-mission/README.md` → `about/our-mission/README.md`
- [x] `top/our-mission/white-paper.md` → `about/our-mission/white-paper.md`
- [x] `top/our-mission/concept-paper.md` → `about/our-mission/concept-paper.md`
- [x] `top/roadmap-2025/README.md` → `about/roadmap/README.md`
- [x] `top/roadmap-2025/roadmap-2024.md` → `about/roadmap/roadmap-2024.md`
- [x] `top/roadmap-2025/roadmap-2023.md` → `about/roadmap/roadmap-2023.md`
- [x] `top/secured-finance-points-sfp-v2/README.md` → `about/sfp-v2.md`
- [x] `top/secured-finance-points-sfp-v2/secured-finance-points-sfp-v1.md` → `about/sfp-v1.md`
- [x] `top/secured-finance-coin-sfc.md` → `about/sfc.md`

## DeFi Fundamentals

- [x] `resources/knowledge-base/README.md` → `defi-fundamentals/README.md`
- [x] `resources/knowledge-base/defi-vs-cefi.md` → `defi-fundamentals/defi-vs-cefi.md`
- [ ] *New file* → `defi-fundamentals/what-is-defi.md`
- [ ] *New file* → `defi-fundamentals/key-defi-concepts.md`
- [ ] *New file* → `defi-fundamentals/blockchain-basics.md`

## USDFC Stablecoin

- [x] `usdfc-stablecoin-protocol/introduction.md` → `usdfc-stablecoin/overview/README.md`
- [x] `usdfc-stablecoin-protocol/beginners-guide.md` → `usdfc-stablecoin/getting-started/README.md`
- [ ] *New file* → `usdfc-stablecoin/getting-started/creating-a-wallet.md`
- [ ] *New file* → `usdfc-stablecoin/getting-started/minting-usdfc.md`
- [ ] *New file* → `usdfc-stablecoin/getting-started/using-stability-pool.md`
- [ ] *New file* → `usdfc-stablecoin/getting-started/redeeming-usdfc.md`
- [x] `usdfc-stablecoin-protocol/protocol-features/README.md` → `usdfc-stablecoin/core-mechanisms/README.md`
- [x] `usdfc-stablecoin-protocol/protocol-features/mint-and-borrow.md` → `usdfc-stablecoin/core-mechanisms/collateralization-system.md`
- [x] `usdfc-stablecoin-protocol/protocol-features/liquidation-with-stability-pool.md` → `usdfc-stablecoin/core-mechanisms/stability-pool-mechanics.md`
- [x] `usdfc-stablecoin-protocol/protocol-features/redemption-as-peg-mechanism.md` → `usdfc-stablecoin/core-mechanisms/redemption-mechanism.md`
- [x] `usdfc-stablecoin-protocol/protocol-features/recovery-mode.md` → `usdfc-stablecoin/core-mechanisms/recovery-mode.md`
- [ ] *New file* → `usdfc-stablecoin/advanced-topics/README.md`
- [ ] *New file* → `usdfc-stablecoin/advanced-topics/liquidation-process.md`
- [ ] *New file* → `usdfc-stablecoin/advanced-topics/price-stability-analysis.md`
- [ ] *New file* → `usdfc-stablecoin/advanced-topics/risk-management.md`
- [x] `usdfc-stablecoin-protocol/faqs.md` → `usdfc-stablecoin/faqs.md`
- [x] `usdfc-stablecoin-protocol/trove-management.md` → `usdfc-stablecoin/trove-management.md`
- [x] `usdfc-stablecoin-protocol/protocol-fees.md` → `usdfc-stablecoin/protocol-fees.md`
- [x] `usdfc-stablecoin-protocol/deployed-contracts.md` → `usdfc-stablecoin/deployed-contracts.md`
- [x] `usdfc-stablecoin-protocol/community-resources.md` → `usdfc-stablecoin/community-resources.md`

## Fixed-Rate Lending

- [x] `fixed-rate-lending-protocol/introduction.md` → `fixed-rate-lending/overview/README.md`
- [x] `fixed-rate-lending-protocol/beginners-guide.md` → `fixed-rate-lending/getting-started/README.md`
- [ ] *New file* → `fixed-rate-lending/getting-started/lending-assets.md`
- [ ] *New file* → `fixed-rate-lending/getting-started/borrowing-assets.md`
- [ ] *New file* → `fixed-rate-lending/getting-started/managing-positions.md`
- [x] `fixed-rate-lending-protocol/protocol-features/README.md` → `fixed-rate-lending/core-mechanisms/README.md`
- [x] `fixed-rate-lending-protocol/protocol-features/zero-coupon-standard/README.md` → `fixed-rate-lending/core-mechanisms/zero-coupon-bonds-explained.md`
- [x] `fixed-rate-lending-protocol/protocol-features/on-chain-orderbook-system.md` → `fixed-rate-lending/core-mechanisms/order-book-mechanics.md`
- [x] `fixed-rate-lending-protocol/zero-coupon-bond-tokenization.md` → `fixed-rate-lending/core-mechanisms/tokenization-process.md`
- [ ] *New file* → `fixed-rate-lending/advanced-topics/README.md`
- [ ] *New file* → `fixed-rate-lending/advanced-topics/yield-curve-formation.md`
- [x] `resources/knowledge-base/apr-vs-apy.md` → `fixed-rate-lending/advanced-topics/apr-apy-calculations.md`
- [ ] *New file* → `fixed-rate-lending/advanced-topics/market-dynamics.md`
- [x] `fixed-rate-lending-protocol/platform-navigation/*` → `fixed-rate-lending/platform-guide/*`
- [x] `fixed-rate-lending-protocol/protocol-security-and-safety/*` → `fixed-rate-lending/protocol-security-and-safety/*`
- [x] `fixed-rate-lending-protocol/faqs.md` → `fixed-rate-lending/faqs.md`
- [x] `fixed-rate-lending-protocol/protocol-fees.md` → `fixed-rate-lending/protocol-fees.md`
- [x] `fixed-rate-lending-protocol/deployed-contracts.md` → `fixed-rate-lending/deployed-contracts.md`

## Developer Resources

- [ ] *New file* → `developer-resources/README.md`
- [ ] *New file* → `developer-resources/api-documentation.md`
- [ ] *New file* → `developer-resources/sdk-integration.md`
- [x] `fixed-rate-lending-protocol/deployed-contracts.md` → `developer-resources/smart-contract-references/lending-protocol-contracts.md`
- [x] `usdfc-stablecoin-protocol/deployed-contracts.md` → `developer-resources/smart-contract-references/usdfc-contracts.md`
- [x] `fixed-rate-lending-protocol/the-graph/*` → `developer-resources/the-graph/*`
- [x] `fixed-rate-lending-protocol/on-chain-orderbook-deep-dive/*` → `developer-resources/orderbook-deep-dive/*`

## Media Kit

- [x] `resources/brand-assets/*` → `media-kit/*`

## Contact

- [x] `resources/contact-us.md` → (remains as) `resources/contact-us.md`

## Knowledge Base Articles Redistributed

- [x] `resources/knowledge-base/defi-vs-cefi.md` → `defi-fundamentals/defi-vs-cefi.md`
- [x] `resources/knowledge-base/apr-vs-apy.md` → `fixed-rate-lending/advanced-topics/apr-apy-calculations.md`
- [ ] `resources/knowledge-base/zc-bond-price-to-apr.md` → To be moved in future content updates
- [ ] `resources/knowledge-base/discount-factor.md` → To be moved in future content updates
- [ ] `resources/knowledge-base/gas-cost.md` → To be moved in future content updates
- [ ] `resources/knowledge-base/dao.md` → To be moved in future content updates
