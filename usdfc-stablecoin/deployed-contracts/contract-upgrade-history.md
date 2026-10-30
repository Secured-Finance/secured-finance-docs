# ⛑️ Contract Upgrade History

## 30 October 2026 — Filecoin contract update

USDFC contracts were upgraded on Filecoin to improve accounting precision, oracle safeguards and signature validation.

* Improved pending-debt redistribution and Stability Pool accounting, including rounding during withdrawals.
* Opening a Trove, increasing debt and withdrawing collateral now require a current primary-oracle price. When a fallback or last accepted price is used, adding collateral and repaying debt remain available, subject to existing price-freshness and protocol checks.
* Strengthened ProtocolToken permit validation and disabled the unused initializer in the LockupContractFactory implementation.

No token or Trove migration is required.

### Execution

* 30 October 2026, 04:28 UTC — [Five-contract upgrade](https://filecoin.blockscout.com/tx/0x06e624467986ec19cb0cb77f640ab73fad876ef7086663ade9c2b25dafa9e762).
* 30 October 2026, 07:29 UTC — [LockupContractFactory upgrade](https://filecoin.blockscout.com/tx/0x7a91e30f7907abe86f632c2c07caa2c6fb832a1461c08ea9ec61547a04cfbdda).

Code changes: [#49](https://github.com/Secured-Finance/stablecoin-contracts/pull/49), [#52](https://github.com/Secured-Finance/stablecoin-contracts/pull/52), [#54](https://github.com/Secured-Finance/stablecoin-contracts/pull/54), [#56](https://github.com/Secured-Finance/stablecoin-contracts/pull/56), [#58](https://github.com/Secured-Finance/stablecoin-contracts/pull/58).

## September 2026 - Filecoin oracle update

Following the discontinuation of Pyth price oracle support on Filecoin, USDFC migrated to RedStone as its primary oracle. The update also included a contract upgrade to adjust parameters.

### Execution status

Both transactions were successfully executed through the Safe multisig wallet on Filecoin.

[View transaction 1](https://filecoin.blockscout.com/tx/0xf89996f3e6ec700423cd52292bc7f7b3c0d773d443ab0f059ae7db422adaecda)

[View transaction 2](https://filecoin.blockscout.com/tx/0x498cee683867d99cbc9e19d44dadee5a038565e25a8b45ca89af141827dcb513)

Last updated: 30 October 2026 (UTC).
