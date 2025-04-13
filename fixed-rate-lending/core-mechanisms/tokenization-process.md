---
description: Enhancing Liquidity and Composability
---

# 🪙 Zero-Coupon Bond Tokenization

Our protocol allows Zero Coupon Bonds (Lending positions) to be tokenized as ERC20 standard tokens, which is called `ZCToken`, and withdrawn from the platform.

The tokenization flows are the following.

* For token withdrawal:

<figure><img src="../.gitbook/assets/ZCToken mint.png" alt=""><figcaption></figcaption></figure>

* For token deposit

<figure><img src="../.gitbook/assets/ZCToken burn.png" alt=""><figcaption></figcaption></figure>

Each ZC token has a maturity, but if the maturity is 0, it becomes a ZC perpetual token. Generally ZC tokens are minted from `FutureValueVault` but ZC perpetual tokens are minted from `GenesisValueVault`. Please check the [Genesis Value page](on-chain-orderbook-deep-dive/genesis-value.md) for the reference.

**Those token names and symbols are defined as follows: (example as March2024 expire)**

<table data-full-width="false"><thead><tr><th width="96">Asset</th><th width="184">ZC Token Name </th><th width="167" align="center">ZC Token Symbol </th><th width="157" align="center">ZC Perpetual Token Name</th><th>ZC Perpetual Token Symbol</th></tr></thead><tbody><tr><td>ETH</td><td>ZC ETH MAR2024</td><td align="center">zcETH-2024-03</td><td align="center">ZC ETH</td><td>zcETH</td></tr><tr><td>WBTC</td><td>ZC WBTC MAR2024</td><td align="center">zcWBTC-2024-03</td><td align="center">ZC WBTC</td><td>zcWBTC</td></tr><tr><td>USDC</td><td>ZC USDC MAR2024</td><td align="center">zcUSDC-2024-03</td><td align="center">ZC USDC</td><td>zcUSDC</td></tr><tr><td>axlFIL</td><td>ZC axlFIL MAR2024</td><td align="center">zcaxlFIL-2024-03</td><td align="center">ZC axlFIL</td><td>zcaxlFIL</td></tr></tbody></table>

**Metamask Symbol Name Convention with max 11 chars:(example as March2024 expire)**

| Asset  | ZC Token Name     | Metamask Symbol  |
| ------ | ----------------- | ---------------- |
| ETH    | ZC ETH MAR2024    | zcETH24M         |
| WBTC   | ZC WBTC MAR2024   | zcWBTC24M        |
| USDC   | ZC USDC MAR2024   | zcUSDC24M        |
| axlFIL | ZC axlFIL MAR2024 | zcxFIL24M        |
| FIL    | ZC FIL MAR2024    | zcFIL24M         |

MAR = M; JUN = J; SEP = S; DEC = D
