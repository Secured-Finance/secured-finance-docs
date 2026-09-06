---
description: Deployed contract addresses, token standards, and audit reports
---

# 📔 Contracts and Security

## Contract addresses

The latest version of [`@secured-finance/stablecoin-contracts`](https://github.com/Secured-Finance/stablecoin-contracts) is deployed at the addresses below. **Always verify addresses against this page before interacting with the contracts directly.**

### USDFC token

| Network | Address |
| --- | --- |
| Filecoin Mainnet | [`0x80B98d3aa09ffff255c3ba4A241111Ff1262F045`](https://filfox.info/en/address/0x80B98d3aa09ffff255c3ba4A241111Ff1262F045) |
| Filecoin Calibration Testnet | [`0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0`](https://calibration.filfox.info/en/address/0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0) |

### Protocol contracts (Filecoin Mainnet)

<!-- TODO(マージ前): RedStoneのFIL/USDフィードアドレスを確認して1行追加（例：RedStone FIL/USD feed | Primary oracle | アドレス） -->

| Contract | Role | Address |
| --- | --- | --- |
| BorrowerOperations | Opening, adjusting, and closing Troves | [`0x1dE3c2e21DD5AF7e5109D2502D0d570D57A1abb0`](https://filfox.info/en/address/0x1dE3c2e21DD5AF7e5109D2502D0d570D57A1abb0) |
| TroveManager | Liquidations, redemptions, Trove state | [`0x5aB87c2398454125Dd424425e39c8909bBE16022`](https://filfox.info/en/address/0x5aB87c2398454125Dd424425e39c8909bBE16022) |
| StabilityPool | Stability Pool deposits and gains | [`0x791Ad78bBc58324089D3E0A8689E7D045B9592b5`](https://filfox.info/en/address/0x791Ad78bBc58324089D3E0A8689E7D045B9592b5) |
| PriceFeed | FIL/USD price with fallback logic | [`0x80e651c9739C1ed15A267c11b85361780164A368`](https://filfox.info/en/address/0x80e651c9739C1ed15A267c11b85361780164A368) |
| TellorCaller | Fallback oracle adapter | [`0x3eA890431C85F40405BBF5BE74D03802672aFe3b`](https://filfox.info/en/address/0x3eA890431C85F40405BBF5BE74D03802672aFe3b) |
| ActivePool | Collateral and debt of active Troves | [`0x8637Ac7FdBB4c763B72e26504aFb659df71c7803`](https://filfox.info/en/address/0x8637Ac7FdBB4c763B72e26504aFb659df71c7803) |
| DefaultPool | Redistributed collateral and debt | [`0xAda716f497da8EC9F766F9a94779E1b6e73d29fF`](https://filfox.info/en/address/0xAda716f497da8EC9F766F9a94779E1b6e73d29fF) |
| CollSurplusPool | Claimable collateral surpluses from liquidations | [`0x212799bEA5c2ed87D84b9Ae3C1Fb0fdc1bFC7AE9`](https://filfox.info/en/address/0x212799bEA5c2ed87D84b9Ae3C1Fb0fdc1bFC7AE9) |
| GasPool | Holds Liquidation Reserves | [`0xbd73175383ac35b2BfdD89377D9D8BDC11dA1bF8`](https://filfox.info/en/address/0xbd73175383ac35b2BfdD89377D9D8BDC11dA1bF8) |
| SortedTroves | Troves ordered by collateral ratio | [`0x2C32e48e358d5b893C46906b69044D342d8DDd5F`](https://filfox.info/en/address/0x2C32e48e358d5b893C46906b69044D342d8DDd5F) |
| HintHelpers | Gas-efficient operation hints | [`0xf06A4eBa3B9e45533566a31DA2F213bc44E89E60`](https://filfox.info/en/address/0xf06A4eBa3B9e45533566a31DA2F213bc44E89E60) |
| MultiTroveGetter | Batch Trove queries | [`0x5065b1F44fEF55Df7FD91275Fcc2D7567F8bf98F`](https://filfox.info/en/address/0x5065b1F44fEF55Df7FD91275Fcc2D7567F8bf98F) |
| ProtocolTokenStaking | Fee Reserve — receives protocol fees | [`0xc8707b3d426E7D7A0706C48dcd1A4b83bc220dB3`](https://filfox.info/en/address/0xc8707b3d426E7D7A0706C48dcd1A4b83bc220dB3) |


Testnet addresses for every contract are in the repository's [`deployments/outputs`](https://github.com/Secured-Finance/stablecoin-contracts/tree/develop/deployments/outputs).

## Token standards

USDFC implements:

* **ERC-20** — the standard token interface.
* **EIP-2612 (`permit`)** — signature-based approvals, so an approval doesn't require its own transaction.
* **EIP-3009 (`transferWithAuthorization` / `receiveWithAuthorization`)** — signature-authorized transfers that anyone can submit and pay gas for, enabling gasless transfers and **x402** payment flows.

EIP-2612 and EIP-3009 support was added by a contract upgrade in September 2025 (the token address did not change) and audited by Hexens in August 2025 — the third report below.

## Audit reports

| Auditor | Date | Scope | Report |
| --- | --- | --- | --- |
| Hexens | 2024/12/30 – 2025/1/20 | Core protocol | [2025-1-Hexens.pdf](https://github.com/Secured-Finance/stablecoin-contracts/blob/develop/audits/2025-01-Hexens.pdf) |
| Decurity | 2025/2/19 – 2025/3/5 | Core protocol | [2025-3-Decurity.pdf](https://github.com/Secured-Finance/stablecoin-contracts/blob/develop/audits/2025-03-Decurity.pdf) |
| Hexens | 2025/8/20 – 2025/8/28 | EIP-3009 / EIP-2612 token upgrade | [2025-8-Hexens.pdf](https://github.com/Secured-Finance/stablecoin-contracts/blob/develop/audits/2025-08-Hexens.pdf) |

## Stress test

[Stress-Testing Simulation and Risk Assessment](https://medium.com/cryptoeconlab/stress-testing-usdfc-8b068d13a1cf) by the CryptoEconLab team:

{% file src="../.gitbook/assets/Secure_Finance_Report.pdf" %}

{% hint style="warning" %}
Audits reduce risk but never eliminate it. The protocol's price feed also currently depends on update jobs operated by Secured Finance — see [Price Oracle](core-mechanics/price-oracle.md) for the trust assumptions.
{% endhint %}
