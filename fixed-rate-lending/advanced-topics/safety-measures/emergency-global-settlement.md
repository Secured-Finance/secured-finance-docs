---
description: A protocol-wide safety mechanism for extreme scenarios in the Fixed-Rate Lending Protocol
icon: 🌎
---

# 🌎 Emergency Global Settlement

## Overview

Emergency global settlement is a critical functionality designed to address unforeseen situations such as hacks or unexpected bugs that could compromise the integrity of our protocol. When this functionality is executed by an admin, all markets are immediately halted, and the protocol becomes non-operational. Subsequently, users can only redeem their positions and withdraw their tokens.

## What You'll Learn

- How Emergency Global Settlement protects the protocol in extreme scenarios
- The step-by-step process of Emergency Global Settlement
- How user positions and deposits are handled during settlement
- How token replacement and withdrawal work after settlement
- How this safety mechanism ensures the security of user funds

## The Emergency Global Settlement Process

1. Admin initiates an emergency global settlement.&#x20;
   * All markets and the Token Vault are brought to a stop.
   * Caches of all price feeds are taken for reference.
2. Users execute redemptions.
   * The collateral token ratios in the Token Vault are calculated.
   * Users' total assets and positions in the Present Value (PV) are computed using the price feed caches. Based on the ratios, their assets and positions are replaced with collateral tokens.
   * Positions of users are reset after the replacement.
3. Users can then withdraw the replaced tokens after redeeming them.

It's important to note that even users who only have deposits without positions will have their deposits replaced with collateral tokens based on the ratios in the Token Vault.



***

### Example Scenario

Let's illustrate the emergency global settlement process with the following example:

**Token Vault Holdings:**

* Total USDC: $100,000
* Equivalent ETH Value: $200,000

_Ratio: 1 USDC to 2 USD worth of ETH_

**User's Positions and Deposits:**

* ETH and FIL Lending Positions (PV value: $10,000)
* ETH Deposits (Valued at $5,000)

_Total Funds: $15,000_



**After Emergency Global Settlement:**

* The user's lending positions and deposits are reset.
* The user receives tokens worth $5,000 of USDC and ETH valued at $10,000 as per the replacement.
* The user can withdraw $5,000 in USDC and $10,000 worth of ETH from their account.



{% hint style="info" %}
Emergency global settlement acts as a vital safeguard, protecting both user funds and the overall integrity of the protocol in unforeseen circumstances. It ensures a secure and resilient DeFi ecosystem for all participants, enhancing trust and confidence in the platform.
{% endhint %}

## FAQ

### When would Emergency Global Settlement be triggered?

Emergency Global Settlement would be triggered in the following scenarios:
1. **Critical Security Breach**: If the protocol experiences a significant hack or security vulnerability
2. **Severe Smart Contract Bug**: If a critical bug is discovered that could compromise user funds
3. **Systemic Risk**: If there's a risk of cascading failures that could affect the entire protocol
4. **Oracle Failure**: If price feeds become compromised or unreliable for an extended period
5. **Governance Decision**: If the protocol governance votes to initiate settlement due to extraordinary circumstances

### What happens to my positions during Emergency Global Settlement?

During Emergency Global Settlement:
1. All markets are immediately halted
2. Your positions are valued using the cached price feeds at the time of settlement
3. Your positions and deposits are converted to collateral tokens based on the ratios in the Token Vault
4. You can then withdraw these tokens after the redemption process
5. No new positions can be created until the protocol is restarted (if ever)

### Can I lose money during Emergency Global Settlement?

While Emergency Global Settlement is designed to be fair to all users:
1. You will receive the proportional value of your positions based on the Token Vault ratios
2. If the Token Vault has insufficient funds (e.g., due to a hack), you may receive less than your full position value
3. The settlement uses cached price feeds, which might differ slightly from market prices at that moment
4. You won't be able to maintain your exact position structure (e.g., specific lending positions)
5. There may be some slippage in value compared to normal market operations

### How do I claim my funds after Emergency Global Settlement?

To claim your funds after Emergency Global Settlement:
1. Connect your wallet to the protocol interface
2. Navigate to the Emergency Settlement section
3. Execute the redemption process to convert your positions to collateral tokens
4. Withdraw your collateral tokens to your wallet
5. This process can typically be completed in a single transaction

### Can Emergency Global Settlement be reversed?

No, Emergency Global Settlement cannot be reversed:
1. It is a one-way process designed as a last-resort safety measure
2. Once triggered, all markets remain permanently closed
3. The protocol would need to be redeployed with new contracts if operations were to resume
4. This irreversibility ensures that users can safely withdraw their funds without concerns about further protocol changes
5. It provides certainty during uncertain circumstances

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Settlement Trigger | Who can initiate emergency settlement | Protocol Admin only |
| Price Feed Cache | How price feeds are stored during settlement | Snapshot at settlement time |
| Redemption Window | Time users have to redeem positions | Unlimited (no expiration) |
| Token Replacement | How positions are converted to tokens | Based on Token Vault ratios |
| Market Status | State of markets after settlement | Permanently closed |

## Related Resources

- [Safety Measures](README.md)
- [Circuit Breaker](circuit-breaker/README.md)
- [Base Price Adjustment](base-price-adjustment.md)
- [Core Mechanics](../../core-mechanics/README.md)
