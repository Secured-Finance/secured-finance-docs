---
description: Deployed addresses, audit reports, and security resources
---

# Contracts & Security

## Contract addresses

The latest version of [`@secured-finance/contracts`](https://github.com/Secured-Finance/contracts) is deployed at the following addresses on **Ethereum Mainnet, Arbitrum One, and Filecoin** (all addresses on this page are taken from the [`deployments/`](https://github.com/Secured-Finance/contracts/tree/develop/deployments) records in the contracts repository):

| Contract | Address |
| --- | --- |
| [BeaconProxyController](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/BeaconProxyController.sol) | `0x581e463841bD2B30285929448e1A93D74708719F` |
| [CurrencyController](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/CurrencyController.sol) | `0x7dca6b6BF30cd28ADe83e86e21e82e3F852bF2DC` |
| [GenesisValueVault](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/GenesisValueVault.sol) | `0xa2700D5feDB13b86Bba3228008C7a0d464a07f2b` |
| [LendingMarketController](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/LendingMarketController.sol) | `0x35e9D8e0223A75E51a67aa731127C91Ea0779Fe2` |
| [ReserveFund](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/ReserveFund.sol) | `0xD2683E22331B9a6e9F38350d829dBEB64ad2778e` |
| [TokenVault](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/TokenVault.sol) | `0xB74749b2213916b1dA3b869E41c7c57f1db69393` |

{% hint style="info" %}
[`ProxyController`](https://github.com/Secured-Finance/contracts/blob/develop/contracts/protocol/ProxyController.sol) is deployed at a **different address on each network**:
{% endhint %}

| Network | ProxyController |
| --- | --- |
| Ethereum Mainnet | `0x5615074Bcd7eA63f10f961064F9EBb8Af61Fa960` |
| Arbitrum One | `0x8A5a80bca08dD11d5623862B8B0f6286f539dFAb` |
| Filecoin | `0x1634D2104B48299DA7D927C4582EA7Ba67020EBB` |

<details>

<summary>Testnet addresses (Sepolia, Arbitrum Sepolia)</summary>

Testnet deployments use different addresses from production:

| Contract | Sepolia | Arbitrum Sepolia |
| --- | --- | --- |
| BeaconProxyController | `0xaa38CeF2FBa6F54Ce1cCe9De7035abCEfE4657a0` | `0x7c221f83b09cA6cA6f89405F4010B307c0B55595` |
| CurrencyController | `0x5b82FA84e455F7Ba27Def020F18Dc379AB701f97` | `0xe36a7122940d0f530c8857dF37dBaAb2d7D17fC3` |
| GenesisValueVault | `0x89fF7044d93bA01b6cEE2eBA09D0f793A8533704` | `0x087b6E8728C39D298F39d22E1Ceb95E8d0e72B3F` |
| LendingMarketController | `0x66aCc8c1314797fDba0b63676C8Aa367D3821C8C` | `0xc81ec45EDb30b755f66D050AdEB77cC85522e794` |
| ProxyController | `0xE453FfcA365a46eaf5b3D5752b5Dc87Fc6986cd8` | `0xE9bDa3831905ABB5f2Ba50D6A23Bf22e5f539E00` |
| ReserveFund | `0x4f856edE4846f1dC6A2cD4a452b3E704C61f1134` | `0x20b24b5A5e45bB27e36B95E1578b13975db19b52` |
| TokenVault | `0x4E01afFD15C58221faC3F77649a483531fF13646` | `0xB61ec7d5bE3bEdc038bd5f4E32e870B83F725F37` |

</details>

<details>

<summary>Deprecated networks (Avalanche, Polygon zkEVM)</summary>

Avalanche support is deprecated. Polygon zkEVM has been sunset and is no longer operational. The legacy deployment addresses below are retained for historical reference only.

Avalanche legacy addresses:

| Contract | Address |
| --- | --- |
| BeaconProxyController | `0x581e463841bD2B30285929448e1A93D74708719F` |
| CurrencyController | `0x7dca6b6BF30cd28ADe83e86e21e82e3F852bF2DC` |
| GenesisValueVault | `0xa2700D5feDB13b86Bba3228008C7a0d464a07f2b` |
| LendingMarketController | `0x35e9D8e0223A75E51a67aa731127C91Ea0779Fe2` |
| ProxyController | `0x0fC649b763A685E2f22fA248CEbf6b2b70f53F1F` |
| ReserveFund | `0xD2683E22331B9a6e9F38350d829dBEB64ad2778e` |
| TokenVault | `0xB74749b2213916b1dA3b869E41c7c57f1db69393` |

Polygon zkEVM legacy addresses:

| Contract | Address |
| --- | --- |
| BeaconProxyController | `0xd5043054819F001B40F13dDCB3EA5aCa9bc18947` |
| CurrencyController | `0x9E1254292195F241FA2DF1aA51af23796627A74B` |
| GenesisValueVault | `0x5926A0F0D204444bEDfa16F3Ae51C26848245402` |
| LendingMarketController | `0x9a2B4b3AC4AE0D8aFE670DacB639e71C81f7Ba36` |
| ProxyController | `0x54A3F4ef9854c43926563348508d1E9C0f1D7926` |
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
