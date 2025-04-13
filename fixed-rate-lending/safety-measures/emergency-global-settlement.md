---
description: A Safety Net for Unforeseen Situations
---

# 🌎 Emergency Global Settlement

Emergency global settlement is a critical functionality designed to address unforeseen situations such as hacks or unexpected bugs that could compromise the integrity of our protocol. When this functionality is executed by an admin, all markets are immediately halted, and the protocol becomes non-operational. Subsequently, users can only redeem their positions and withdraw their tokens.

### The Emergency Global Settlement process:

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
