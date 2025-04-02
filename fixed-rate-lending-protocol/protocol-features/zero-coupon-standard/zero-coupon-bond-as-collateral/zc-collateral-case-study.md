---
description: Navigating Utilization Ratios and ZC collateral Liquidation Process
---

# 🏍️ ZC Collateral Case Study

This case study aims to elucidate the practical application of Zero Coupon Bonds (ZC) as collateral within our platform, focusing on the calculation of ZC utilization ratios, the overall collateral utilization ratio, and ZC collateral liquidation. Through a detailed example, we will explore how these metrics are displayed and calculated, providing insights into effective collateral management.

### **Example Scenario: Leveraging ZC Bonds Without Cash Collateral**

Consider an user A who holds a ZC bond with a Present Value (PV) of 1,000 USDC. Opting to use this ZC bond as collateral, the user A seeks to borrow without pledging any cash collateral. Under our platform's guidelines, he is eligible to borrow up to 80% of the ZC's PV, equating to 800 USDC.

Upon borrowing the 800 USDC, the ZC utilization ratio for the user A reaches 80%, reflecting the proportion of the ZC bond's value that has been leveraged. However, the total collateral utilization ratio presents a more comprehensive view of his position.

### **Calculating Total Collateral Utilization Ratio**

The total collateral utilization ratio is calculated by considering both the borrowed amount and the utilized ZC as part of the collateral base. This calculation is crucial for understanding the full scope of collateral engagement on the platform. In this scenario, the formula is applied as follows:



$$
\text{Collateral Utilization Ratio} = \frac{\text{Obligation}}{\text{Cash Collateral} + \text{Utilized ZC}}
$$

Given that the his obligation is 800 USDC and the utilized ZC amounts to 1,000 USDC, the presence of the borrowed 800 USDC as part of the collateral (under the Secured Finance Vault) modifies the equation. Thus, the total collateral base is the sum of the ZC's PV and the borrowed cash, totaling 1800 USDC. The calculation becomes:&#x20;



$$
\text{Collateral Utilization Ratio} = \frac{800}{1,000 + 800} = 44.44\%
$$

This results in a collateral utilization ratio of approximately 44.44%, illustrating a more favorable leverage position than indicated by the ZC utilization ratio alone.&#x20;

In the scenario described, User A has the capability to withdraw up to 800 USDC cash into their wallet. Consequently, both the ZC utilization and the overall Collateral utilization ratios stand at 80%. It's crucial to remain vigilant regarding potential sudden fluctuations in the ZC bond price. Should these ratios exceed 80%, it would initiate a liquidation process.



### Case Study: Liquidation of ZC Collateral

In this scenario, let's consider User A, who has utilized a Zero Coupon Bond (ZC) as collateral to borrow funds. User A successfully borrows 800 USDC, which leads to a ZC utilization of 80% and a collateral utilization also at 80% without any cash collateral position.&#x20;

**Liquidation Mechanics**

Should the price of the ZC bond experience a sudden decline, the liquidation process may be initiated. Same as the normal liquidation process, the liquidator is permitted to liquidate up to 50% of User A's obligation, which amounts to a maximum of 400 USDC. The liquidation process involves User A losing a portion of their collateral equal to the liquidated amount plus a liquidation fee. The total cost to User A, including the liquidation fee of 7% (5%:fee for liquidator, and 2%:reserve fund), would be 428 USDC (400 USDC + 28 USDC).

**Post-Liquidation Position**

After the liquidation, User A's remaining obligation is reduced to 400 USDC, while the ZC collateral is diminished to 572 USDC (1000 USDC original collateral - 428 USDC liquidated amount). Consequently, the ZC utilization ratio post-liquidation adjusts to approximately 69.93%, calculated as follows:

$$
\text{ZC Utilization Ratio} = \frac{400}{572} \approx 69.93\%
$$

\
