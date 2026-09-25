# ⛑️ Contract Upgrade History

## September 2026 upgrade

The engineering team confirmed execution on Ethereum Mainnet, Arbitrum One and Filecoin on 24 September 2026 (UTC).

Source reference: Contracts PR #435, merged into develop on 24 September 2026.

[Contracts PR #435 - view changes on GitHub](contract-upgrade-history.md#september-2026-upgrade)

Merge commit: 68d29760d53891f8a4e89069b1de6831febea54b



Changes include revised order-book tree removal and rebalancing, chunk metadata, order-price and growth limits, batched Itayose, recovery tooling, and TokenVault safeguards. Inclusion of recovery tools does not mean recovery has been executed for every position.

### Ethereum Mainnet

Ethereum: successful execution on 24 September 2026 at 22:47:59 UTC, block 26,050,390.

[View Ethereum transaction](contract-upgrade-history.md#september-2026-upgrade)

### Arbitrum One

Arbitrum: successful execution on 24 September 2026 at 23:11:00 UTC, block 508,590,941.

[View Arbitrum transaction](contract-upgrade-history.md#september-2026-upgrade)

### Filecoin

Filecoin: two multisig execution messages, both Applied: true; Code: 0.

[View Filecoin execution 49](contract-upgrade-history.md#september-2026-upgrade)

Filecoin execution 50: https://www.glif.io/en/tx/bafy2bzacebkbpgyn5vpvegaowusje5gy37uh2t2aw5wapcnegfo5px54xh35a



These source and execution references are not an independent audit certificate. Integrators should check deployed implementations and corresponding ABIs. Earlier upgrades can be inspected via explorer Past Implementations views and controller upgrade events.

## 25 September 2026 - Filecoin oracle updates

These updates were executed separately from the lending contract upgrade above.

### Lending price feeds

Fixed-Rate Lending: three multisig proposals updated the price feeds for FIL, iFIL and wpFIL. Execution IDs 51, 52 and 53 each returned Applied: true; Code: 0.

Execution 51: https://www.glif.io/en/tx/bafy2bzaced6snlpq4qllbijh2wegxplsp45yifhiccuuzp5olayzatxlujiiy

[View execution 52](contract-upgrade-history.md#september-2026-upgrade)

[View execution 53](contract-upgrade-history.md#september-2026-upgrade)



### USDFC stablecoin

Related USDFC update (separate product): two Safe transactions implemented the change to use RedStone as the primary oracle, including a contract upgrade to adjust parameters. Both transactions show Success on the explorer.

[Transaction 1 - 25 September 2026, 02:45:00 UTC](https://filecoin.blockscout.com/tx/0xf89996f3e6ec700423cd52292bc7f7b3c0d773d443ab0f059ae7)

[Transaction 2 - 25 September 2026, 02:49:30 UTC](contract-upgrade-history.md#september-2026-upgrade)

These oracle updates do not by themselves establish completion of lending position recovery or market reopening.



Last updated: 25 September 2026 (UTC).



