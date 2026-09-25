# Contract Upgrade History

Contract upgrades and recovery are separate milestones. An upgrade alone does not confirm balance restoration or market reopening.

All dates and times on this page are in UTC.



September 2026 upgrade

The engineering team confirmed execution on Ethereum Mainnet, Arbitrum One and Filecoin on 24 September 2026 (UTC).

Source reference: Contracts PR #435, merged into develop on 24 September 2026.

Pull request: https://github.com/Secured-Finance/contracts/pull/435

Merge commit: 68d29760d53891f8a4e89069b1de6831febea54b



Changes include revised order-book tree removal and rebalancing, chunk metadata, order-price and growth limits, batched Itayose, recovery tooling, and TokenVault safeguards. Inclusion of recovery tools does not mean recovery has been executed for every position.

Ethereum: successful execution on 24 September 2026 at 22:47:59 UTC, block 26,050,390.

Ethereum transaction: https://etherscan.io/tx/0x03a64f5fc22a8e1b58e925509bd5cdc7cb2d0207600388373e64de58a9679204

Arbitrum: successful execution on 24 September 2026 at 23:11:00 UTC, block 508,590,941.

Arbitrum transaction: https://arbiscan.io/tx/0xce98babc6739dfbee481efe13685df3110f6cbb21f22941782ceaaf964edd279

Filecoin: two multisig execution messages, both Applied: true; Code: 0.

Filecoin execution 49: https://www.glif.io/en/tx/bafy2bzaceddjkucs54nmddhjoanmsxw2ayqqllk5onp4asoab2dnrcfbqckcm

Filecoin execution 50: https://www.glif.io/en/tx/bafy2bzacebkbpgyn5vpvegaowusje5gy37uh2t2aw5wapcnegfo5px54xh35a



These source and execution references are not an independent audit certificate. Integrators should check deployed implementations and corresponding ABIs. Earlier upgrades can be inspected via explorer Past Implementations views and controller upgrade events.



25 September 2026 - Additional Filecoin oracle updates

These updates were executed separately from the lending contract upgrade above.

Fixed-Rate Lending: three multisig proposals updated the price feeds for FIL, iFIL and wpFIL. Execution IDs 51, 52 and 53 each returned Applied: true; Code: 0.

Execution 51: https://www.glif.io/en/tx/bafy2bzaced6snlpq4qllbijh2wegxplsp45yifhiccuuzp5olayzatxlujiiy

Execution 52: https://www.glif.io/en/tx/bafy2bzacedoa4i6pmiqtxyc2vlhsajmmui34tgtxyo5xl4uxij2t3p5cl6oqa

Execution 53: https://www.glif.io/en/tx/bafy2bzaced6jvxha36jzpkhrqkyym6fek4sazwcwvqnmpkksikoxxcyzkyzjq



Related USDFC update (separate product): two Safe transactions implemented the change to use RedStone as the primary oracle, including a contract upgrade to adjust parameters. Both transactions show Success on the explorer.

USDFC transaction 1 (25 September 2026, 02:45:00 UTC): https://filecoin.blockscout.com/tx/0xf89996f3e6ec700423cd52292bc7f7b3c0d773d443ab0f059ae7db422adaecda

USDFC transaction 2 (25 September 2026, 02:49:30 UTC): https://filecoin.blockscout.com/tx/0x498cee683867d99cbc9e19d44dadee5a038565e25a8b45ca89af141827dcb513

These oracle updates do not by themselves establish completion of lending position recovery or market reopening.



Last updated: 25 September 2026 (UTC).



