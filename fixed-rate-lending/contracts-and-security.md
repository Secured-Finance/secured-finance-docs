---
description: Deployed addresses, audit reports, and security resources
---

# Contracts & Security

## Contract addresses

The latest version of [`@secured-finance/contracts`](https://github.com/Secured-Finance/contracts) is deployed at the following addresses on **Ethereum Mainnet, Sepolia, Arbitrum One, Arbitrum Sepolia, and Filecoin**:

| Contract | Address |
| --- | --- |
| [BeaconProxyController](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/BeaconProxyController.sol) | `0x581e463841bD2B30285929448e1A93D74708719F` |
| [CurrencyController](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/CurrencyController.sol) | `0x7dca6b6BF30cd28ADe83e86e21e82e3F852bF2DC` |
| [GenesisValueVault](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/GenesisValueVault.sol) | `0xa2700D5feDB13b86Bba3228008C7a0d464a07f2b` |
| [LendingMarketController](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/LendingMarketController.sol) | `0x35e9D8e0223A75E51a67aa731127C91Ea0779Fe2` |
| [ProxyController](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/ProxyController.sol) | `0x1634D2104B48299DA7D927C4582EA7Ba67020EBB` |
| [ReserveFund](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/ReserveFund.sol) | `0xD2683E22331B9a6e9F38350d829dBEB64ad2778e` |
| [TokenVault](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/TokenVault.sol) | `0xB74749b2213916b1dA3b869E41c7c57f1db69393` |

<details>

<summary>Deprecated networks (Avalanche, Polygon zkEVM)</summary>

Support for Avalanche and Polygon zkEVM has been sunset. If you still hold assets there, unwind positions and bridge out. Polygon zkEVM legacy addresses:

| Contract | Address |
| --- | --- |
| BeaconProxyController | `0xd5043054819F001B40F13dDCB3EA5aCa9bc18947` |
| CurrencyController | `0x9E1254292195F241FA2DF1aA51af23796627A74B` |
| GenesisValueVault | `0x5926A0F0D204444bEDfa16F3Ae51C26848245402` |
| LendingMarketController | `0x9a2B4b3AC4AE0D8aFE670DacB639e71C81f7Ba36` |
| ProxyController | `0x0858A345343759554db3ff0698c251E4a138e452` |
| ReserveFund | `0xff56c7d0129a75594D02ee02F73E5538E3171445` |
| TokenVault | `0x0896AC8B9e2DC3545392ff65061E5a8a3eD68824` |

</details>

## Audit reports

| Auditor | Scope | Period | Report |
| --- | --- | --- | --- |
| Quantstamp | Fixed-Rate Lending contracts | 2023/10–11 | [2023-11-Quantstamp.pdf](https://github.com/Secured-Finance/contracts/blob/develop/audits/2023-11-Quantstamp.pdf) |
| Quantstamp | Fixed-Rate Lending contracts | 2024/3 | [2024-03-Quantstamp.pdf](https://github.com/Secured-Finance/contracts/blob/develop/audits/2024-03-Quantstamp.pdf) |

USDFC Stablecoin audits (Hexens 2025/1, Decurity 2025/3) are listed in the [USDFC documentation](../usdfc-stablecoin/deployed-contracts.md).

## Security resources

* **Bug Bounty** — vulnerabilities are rewarded through our [Bug Bounty program](../developer-portal/bug-bounty.md)
* **Runtime protections** — [Circuit Breaker](advanced-topics/circuit-breaker.md), [Base Price Adjustment](advanced-topics/base-price-adjustment.md), and [minimum-volume Mark Pricing](core-concepts/liquidation/mark-to-market.md)
* **Last resort** — [Emergency Global Settlement](advanced-topics/emergency-global-settlement.md)
* **Verify parameters yourself** — on-chain getters listed in [Protocol Parameters](protocol-parameters.md)
