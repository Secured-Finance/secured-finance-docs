# ⛑️ Contract Upgrade History

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

[View Filecoin execution 49](https://www.glif.io/en/tx/bafy2bzaceddjkucs54nmddhjoanmsxw2ayqqllk5onp4asoab2dnrcfbqckcm)

[View Filecoin execution 50](https://www.glif.io/en/tx/bafy2bzacebkbpgyn5vpvegaowusje5gy37uh2t2aw5wapcnegfo5px54xh35a)



These source and execution references are not an independent audit certificate. Integrators should check deployed implementations and corresponding ABIs. Earlier upgrades can be inspected via explorer Past Implementations views and controller upgrade events.

## 25 September 2026 - Filecoin oracle updates

These updates were executed separately from the lending contract upgrade above.

### Lending price feeds

Fixed-Rate Lending: all three price-feed updates for FIL, iFIL and wpFIL were successfully executed through the multisig wallet (transactions 51, 52 and 53).

[View execution 51](https://www.glif.io/en/tx/bafy2bzaced6snlpq4qllbijh2wegxplsp45yifhiccuuzp5olayzatxlujiiy)

[View execution 52](https://www.glif.io/en/tx/bafy2bzacedoa4i6pmiqtxyc2vlhsajmmui34tgtxyo5xl4uxij2t3p5cl6oqa)

[View execution 53](https://www.glif.io/en/tx/bafy2bzaced6jvxha36jzpkhrqkyym6fek4sazwcwvqnmpkksikoxxcyzkyzjq)





These oracle updates do not by themselves establish completion of lending position recovery or market reopening.



Last updated: 25 September 2026 (UTC).



