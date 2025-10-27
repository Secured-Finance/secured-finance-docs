---
description: Understanding the protocol's defensive mechanism to maintain system solvency
---

# 🚨 Recovery Mode

## Overview

Recovery Mode is a critical safety mechanism in the USDFC Stablecoin Protocol that activates when the Total Collateral Ratio (TCR) falls below 150%. It implements stricter rules for borrowing and liquidation to protect the protocol from systemic under-collateralization and restore stability to the system.

{% hint style="warning" %}
When Recovery Mode is active, Troves with collateral ratios below the current TCR become eligible for liquidation, even if they are above the normal 110% minimum threshold. This creates significant risk for borrowers with lower collateral ratios.
{% endhint %}

## How It Works

Recovery Mode is triggered automatically when the protocol's Total Collateral Ratio (TCR) falls below 150%. During this state, the protocol implements several changes to encourage deleveraging and recapitalization:

### Key Changes During Recovery Mode

1. **Elevated Liquidation Threshold**
   * Normal Mode: Troves below 110% collateral ratio are eligible for liquidation
   * Recovery Mode: Troves below the current TCR (which is < 150%) are eligible for liquidation
   * This means a Trove with 140% collateral ratio could be liquidated if the TCR is 145%
2. **Zero Minting Fee**
   * The borrowing fee is reduced to 0% to encourage users to add collateral
   * This makes it more economical to improve collateral ratios by minting additional USDFC
3. **Restricted Borrowing**
   * New borrowing is only allowed if it improves the TCR
   * Users can only mint USDFC if they create a new Trove with ≥150% collateral ratio
   * Existing Trove adjustments are only permitted if they increase the collateral ratio

## Key Parameters

| Parameter             | Normal Mode      | Recovery Mode        |
| --------------------- | ---------------- | -------------------- |
| Liquidation Threshold | 110%             | Current TCR (< 150%) |
| Minting Fee           | Base Rate + 0.5% | 0%                   |
| Minimum New Trove CR  | 110%             | 150%                 |
| System Exit Threshold | N/A              | TCR ≥ 150%           |

## Liquidation Behavior in Recovery Mode

Recovery Mode introduces a more complex liquidation process to maximize system stability:

<table><thead><tr><th width="277">Condition</th><th>Liquidation Behavior</th></tr></thead><tbody><tr><td>ICR ≤ 100%</td><td><strong>Redistribute</strong> all debt and collateral (minus gas compensation) to active Troves.</td></tr><tr><td>100% &#x3C; ICR &#x3C; 110%<br>&#x26;<br>SP USDFC > Trove debt</td><td>USDFC in the Stability Pool equal to the Trove's debt is offset with the Trove's debt. The Trove's FIL collateral (minus gas compensation) is shared between depositors.</td></tr><tr><td>100% &#x3C; ICR &#x3C; 110%<br>&#x26;<br>SP USDFC &#x3C; Trove debt</td><td>The total Stability Pool USDFC is offset with an equal amount of debt from the Trove. A fraction of the Trove's collateral (equal to the ratio of its offset debt to its entire debt) is shared between depositors. The remaining debt and collateral (minus gas compensation) is <strong>redistributed</strong> to active Troves.</td></tr><tr><td>110% ≤ ICR &#x3C; TCR<br>&#x26;<br>SP USDFC >= Trove debt</td><td>The Stability Pool USDFC is offset with an equal amount of debt from the Trove. A fraction of FIL collateral with dollar value equal to <code>1.1 * debt</code> is shared between depositors. Nothing is redistributed to other active Troves. Since its ICR was <code>> 1.1</code>, the Trove has a collateral remainder, which is sent to the <code>CollSurplusPool</code> and is claimable by the borrower. The Trove is closed.</td></tr><tr><td>110% ≤ ICR &#x3C; TCR<br>&#x26;<br>SP USDFC &#x3C; Trove debt</td><td>Do nothing.</td></tr><tr><td>ICR ≥ TCR</td><td>Do nothing.</td></tr></tbody></table>

Where:

* ICR = Individual Collateral Ratio
* MCR = Minimum Collateral Ratio (110%)
* TCR = Total Collateral Ratio
* SP = Stability Pool

## Example Scenario

1. **Triggering Recovery Mode**
   * The TCR falls to 145%, automatically activating Recovery Mode
   * All Troves with collateral ratios below 145% become eligible for liquidation
2. **System Response**
   * Minting fees drop to 0% to encourage collateral additions
   * Borrowers rush to improve their collateral ratios to avoid liquidation
   * Liquidators target Troves with collateral ratios below 145%
3. **Exiting Recovery Mode**
   * As users add collateral and repay debt, the TCR gradually improves
   * Once the TCR exceeds 150%, the system returns to Normal Mode
   * Regular liquidation thresholds (110%) and minting fees are restored

## Risk Management for Borrowers

During Recovery Mode, borrowers should take immediate action to protect their positions:

1. **Add Collateral**: The most direct way to increase your collateral ratio
2. **Repay Debt**: Reducing your debt also improves your collateral ratio
3. **Monitor TCR**: Keep track of the system's TCR to understand your liquidation risk
4. **Maintain Buffer**: Aim for a collateral ratio well above 150% to avoid liquidation risk

{% hint style="success" %}
**Best Practice**: Maintain a collateral ratio of at least 200% during normal operations to provide a substantial buffer against Recovery Mode liquidations.
{% endhint %}

## Common Questions

**How long does Recovery Mode typically last?**\
The duration varies based on market conditions and user behavior. It ends automatically when the TCR returns above 150%.

**Will I be notified if Recovery Mode is activated?**\
The protocol doesn't send direct notifications. You should monitor the protocol's status page or use third-party monitoring tools.

**Can I still close my Trove during Recovery Mode?**\
Yes, you can still close your Trove by repaying all debt, regardless of Recovery Mode status.

[Learn more in the FAQs section](../faqs.md)

## Related Topics

* [The Trove System](../core-mechanics/the-trove-system.md)
* [Liquidation](../core-mechanics/liquidation.md)
* [System Overview](../core-mechanics/system-overview.md)
