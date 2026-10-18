# Incident Recovery & Verification

Fixed-Rate Lending recovery on Ethereum, Arbitrum and Filecoin.

## Recovery status

Markets and TokenVaults reopened on **16 October 2026 (UTC)** following production-state verification. This page records protocol restoration, not a claim that all stolen funds have been recovered.

## Corrections and verification

Recovery work corrected affected positions and aggregate supply, cleared residual order-book entries, and reversed an affected Filecoin USDFC fill. [PR #444](https://github.com/Secured-Finance/contracts/pull/444) documents the residual-order correction; [PR #446](https://github.com/Secured-Finance/contracts/pull/446) removes temporary recovery code.

Verification covered both order-book sides across all initialized maturities. Targeted entries were cleared, observed non-target sides were unchanged, and the Filecoin fill-reversal checks matched expected balances and events.

Final block-specific checks confirmed deployed implementations, removal of temporary recovery access, approved operator roles, and unpaused markets and TokenVaults. These checks establish the recorded production state; they are not an independent security certification or a guarantee against future incidents.

## Supporting records

* Correction transactions: [Ethereum](https://etherscan.io/tx/0x9ca19a16b21fe281821fa33cc4fbbb550db68fb7cfa2d135274763703f41ae26), [Arbitrum](https://arbiscan.io/tx/0x6c6b909247a913e52acf6fdd44f5791b750beed92af6eedee3e8ad4f6ce9b3f6), [Filecoin](https://filecoin.blockscout.com/tx/0x22958d4a14a59f6520795a3cb3b98a6a4d40393a38814119903c4df0c191fbb8).
* [Recovery instructions and manifests — pinned commit](https://github.com/Secured-Finance/contracts/tree/ad0987f0aee40175da7f9f2490c33a7917d2bed1/recovery-data).
* [Contract Upgrade History](https://docs.secured.finance/fixed-rate-lending/contracts-and-security/contract-upgrade-history).

The incident postmortem will be linked here when published.

Last updated: 18 October 2026 (UTC).
