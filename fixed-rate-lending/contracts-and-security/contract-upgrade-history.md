# ⛑️ Contract Upgrade History

## 23 October 2026 upgrade

The Fixed-Rate Lending contracts were upgraded on Ethereum, Arbitrum and Filecoin.

* [PR #447](https://github.com/Secured-Finance/contracts/pull/447) adds configurable minimum pre-order amounts per currency to reduce negligible-value order spam.
* [PR #450](https://github.com/Secured-Finance/contracts/pull/450) improves withdrawal calculations so small borrowing balances remain accounted for and full deposits can be withdrawn when sufficient collateral remains.

No position migration is required. Integrations using `cleanUpAllFunds(address)` should use the currency-specific `cleanUpFunds(bytes32,address)` instead.

Successful executions on 23 October 2026 (UTC):

* [Ethereum Mainnet](https://etherscan.io/tx/0xf4df07a16be0f8bf6afb79172afb9eb0965b1df48c2d3a325b3ec9683ce6c25f) — 00:31:11 UTC
* [Arbitrum One](https://arbiscan.io/tx/0x1410fd6d7a69a0d84c5058d25499fd69454b58f4aa34c5cd6b23524974b3a70b) — 00:31:34 UTC
* [Filecoin](https://filecoin.blockscout.com/tx/0xb56e4cef7f3ca586884913605e0c1aafbe95c715e4d26d3d6f806b2124ebd58b) — 00:32:30 UTC

## October 2026 recovery and reopening

Recovery-related contract updates were executed on Ethereum, Arbitrum and Filecoin. Corrections executed on 15 October under [PR #444](https://github.com/Secured-Finance/contracts/pull/444) cleared residual order-book entries and reversed an affected Filecoin fill. The subsequent [PR #446](https://github.com/Secured-Finance/contracts/pull/446) cleanup removed temporary recovery functionality and restored order-estimation functions.

Cleanup upgrade executions:

* [Ethereum](https://etherscan.io/tx/0xf2450208223b161a4d2242b7823915f164e99d248c7c9aa544283ad5e01c3ca2)
* [Arbitrum](https://arbiscan.io/tx/0x9d7e05e40ef4b294c1730345a27128b46b56c8002ff713dea7934d395df4193f)
* [Filecoin](https://filecoin.blockscout.com/tx/0x6a5943d4c848a01e0ab0b053ced64f40fe301c5e32a4fcccfd391c4e9d412eba)

Markets and TokenVaults reopened on 16 October following production-state verification. See [Incident Recovery & Verification](https://docs.secured.finance/fixed-rate-lending/contracts-and-security/security-and-incident-reports/incident-recovery-and-verification) for the correction results, verification scope and supporting evidence.

Dates are UTC. Execution transactions are distinct from proposal approvals.

## September 2026 upgrade

The engineering team confirmed execution on Ethereum Mainnet, Arbitrum One and Filecoin on 24 September 2026 (UTC).

Source reference: Contracts PR #435, merged into develop on 24 September 2026.

[Contracts PR #435 - view changes on GitHub](https://github.com/Secured-Finance/contracts/pull/435)

Merge commit: 68d29760d53891f8a4e89069b1de6831febea54b

Changes include revised order-book tree removal and rebalancing, chunk metadata, order-price and growth limits, batched Itayose, recovery tooling, and TokenVault safeguards. Inclusion of recovery tools does not mean recovery has been executed for every position.

### Ethereum Mainnet

Ethereum: successful execution on 24 September 2026 at 22:47:59 UTC, block 26,050,390.

[View Ethereum transaction](https://etherscan.io/tx/0x03a64f5fc22a8e1b58e925509bd5cdc7cb2d0207600388373e64de58a9679204)

### Arbitrum One

Arbitrum: successful execution on 24 September 2026 at 23:11:00 UTC, block 508,590,941.

[View Arbitrum transaction](https://arbiscan.io/tx/0xce98babc6739dfbee481efe13685df3110f6cbb21f22941782ceaaf964edd279)

### Filecoin

Filecoin: both upgrade transactions were successfully executed through the multisig wallet.

[View Filecoin execution 49](https://glif.io/en/tx/bafy2bzaceddjkucs54nmddhjoanmsxw2ayqqllk5onp4asoab2dnrcfbqckcm)

[View Filecoin execution 50](https://glif.io/en/tx/bafy2bzacebkbpgyn5vpvegaowusje5gy37uh2t2aw5wapcnegfo5px54xh35a)

These source and execution references are not an independent audit certificate. Integrators should check deployed implementations and corresponding ABIs. Earlier upgrades can be inspected via explorer Past Implementations views and controller upgrade events.

## Filecoin oracle updates

Following the discontinuation of Pyth price oracle support on Filecoin, the Fixed-Rate Lending protocol migrated its FIL, iFIL and wpFIL price feeds to RedStone.

### Lending price feeds

Fixed-Rate Lending: all three price-feed updates for FIL, iFIL and wpFIL were successfully executed through the multisig wallet (transactions 51, 52 and 53).

[View execution 51](https://glif.io/en/tx/bafy2bzaced6snlpq4qllbijh2wegxplsp45yifhiccuuzp5olayzatxlujiiy)

[View execution 52](https://glif.io/en/tx/bafy2bzacedoa4i6pmiqtxyc2vlhsajmmui34tgtxyo5xl4uxij2t3p5cl6oqa)

[View execution 53](https://glif.io/en/tx/bafy2bzaced6jvxha36jzpkhrqkyym6fek4sazwcwvqnmpkksikoxxcyzkyzjq)

Last updated: 23 October 2026 (UTC).
