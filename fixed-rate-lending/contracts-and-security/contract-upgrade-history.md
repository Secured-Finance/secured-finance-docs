# Contract Upgrade History

Contract upgrades and recovery are separate milestones. An upgrade alone does not confirm balance restoration or market reopening.



September 2026 upgrade

The engineering team confirmed execution on Ethereum Mainnet, Arbitrum One and Filecoin on 25 September 2026 (Hong Kong time).



Source reference: Contracts PR #435, merged into develop on 24 September 2026.

{% embed url="https://github.com/Secured-Finance/contracts/pull/435" %}

Merge commit: 68d29760d53891f8a4e89069b1de6831febea54b



Changes include revised order-book tree removal and rebalancing, chunk metadata, order-price and growth limits, batched Itayose, recovery tooling, and TokenVault safeguards. Inclusion of recovery tools does not mean recovery has been executed for every position.



Ethereum: successful execution on 24 September 2026 at 22:47:59 UTC, block 26,050,390.

{% embed url="https://etherscan.io/tx/0x03a64f5fc22a8e1b58e925509bd5cdc7cb2d0207600388373e64de58a9679204" %}

Arbitrum: successful execution on 24 September 2026 at 23:11:00 UTC, block 508,590,941.

{% embed url="https://arbiscan.io/tx/0xce98babc6739dfbee481efe13685df3110f6cbb21f22941782ceaaf964edd279" %}

Filecoin: two multisig execution messages, both Applied: true; Code: 0.

{% embed url="https://www.glif.io/en/tx/bafy2bzaceddjkucs54nmddhjoanmsxw2ayqqllk5onp4asoab2dnrcfbqckcm" %}



These source and execution references are not an independent audit certificate. Integrators should check deployed implementations and corresponding ABIs. Earlier upgrades can be inspected via explorer Past Implementations views and controller upgrade events.



Last updated: 25 September 2026.

Filecoin execution 49: https://www.glif.io/en/tx/bafy2bzaceddjkucs54nmddhjoanmsxw2ayqqllk5onp4asoab2dnrcfbqckcm

Filecoin execution 50: https://www.glif.io/en/tx/bafy2bzacebkbpgyn5vpvegaowusje5gy37uh2t2aw5wapcnegfo5px54xh35a

