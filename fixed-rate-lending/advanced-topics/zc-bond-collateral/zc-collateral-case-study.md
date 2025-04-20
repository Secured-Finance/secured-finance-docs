---
description: Understanding how Zero-Coupon Bonds can be used as collateral and the liquidation process
icon: 🏍️
---

# 🏍️ ZC Collateral Case Study

## Overview

This case study demonstrates the practical application of Zero Coupon Bonds (ZC) as collateral within our platform, focusing on the calculation of ZC utilization ratios, the overall collateral utilization ratio, and ZC collateral liquidation. Through detailed examples, we explore how these metrics are calculated and displayed, providing insights into effective collateral management.

## What You'll Learn

- How Zero-Coupon Bonds can be used as collateral in the Fixed-Rate Lending Protocol
- How to calculate ZC utilization ratios and total collateral utilization ratios
- How the liquidation process works specifically for ZC bond collateral
- How to determine post-liquidation positions and ratios
- How to manage risk when using ZC bonds as collateral

## How It Works

### Leveraging ZC Bonds Without Cash Collateral

Consider User A who holds a ZC bond with a Present Value (PV) of 1,000 USDC. Opting to use this ZC bond as collateral, User A seeks to borrow without pledging any cash collateral. Under our platform's guidelines, they are eligible to borrow up to 80% of the ZC's PV, equating to 800 USDC.

Upon borrowing the 800 USDC, the ZC utilization ratio for User A reaches 80%, reflecting the proportion of the ZC bond's value that has been leveraged. However, the total collateral utilization ratio presents a more comprehensive view of their position.

### Calculating Total Collateral Utilization Ratio

The total collateral utilization ratio is calculated by considering both the borrowed amount and the utilized ZC as part of the collateral base. This calculation is crucial for understanding the full scope of collateral engagement on the platform. In this scenario, the formula is applied as follows:

$$
\text{Collateral Utilization Ratio} = \frac{\text{Obligation}}{\text{Cash Collateral} + \text{Utilized ZC}}
$$

Given that User A's obligation is 800 USDC and the utilized ZC amounts to 1,000 USDC, the presence of the borrowed 800 USDC as part of the collateral (under the Secured Finance Vault) modifies the equation. Thus, the total collateral base is the sum of the ZC's PV and the borrowed cash, totaling 1,800 USDC. The calculation becomes:

$$
\text{Collateral Utilization Ratio} = \frac{800}{1,000 + 800} = 44.44\%
$$

This results in a collateral utilization ratio of approximately 44.44%, illustrating a more favorable leverage position than indicated by the ZC utilization ratio alone.

In the scenario described, User A has the capability to withdraw up to 800 USDC cash into their wallet. Consequently, both the ZC utilization and the overall Collateral utilization ratios stand at 80%. It's crucial to remain vigilant regarding potential sudden fluctuations in the ZC bond price. Should these ratios exceed 80%, it would initiate a liquidation process.

### Liquidation of ZC Collateral

In this scenario, User A has utilized a Zero Coupon Bond (ZC) as collateral to borrow funds. User A successfully borrows 800 USDC, which leads to a ZC utilization of 80% and a collateral utilization also at 80% without any cash collateral position.

#### Liquidation Mechanics

Should the price of the ZC bond experience a sudden decline, the liquidation process may be initiated. Same as the normal liquidation process, the liquidator is permitted to liquidate up to 50% of User A's obligation, which amounts to a maximum of 400 USDC. The liquidation process involves User A losing a portion of their collateral equal to the liquidated amount plus a liquidation fee. The total cost to User A, including the liquidation fee of 7% (5%: fee for liquidator, and 2%: reserve fund), would be 428 USDC (400 USDC + 28 USDC).

#### Post-Liquidation Position

After the liquidation, User A's remaining obligation is reduced to 400 USDC, while the ZC collateral is diminished to 572 USDC (1000 USDC original collateral - 428 USDC liquidated amount). Consequently, the ZC utilization ratio post-liquidation adjusts to approximately 69.93%, calculated as follows:

$$
\text{ZC Utilization Ratio} = \frac{400}{572} \approx 69.93\%
$$

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Maximum ZC Utilization | Maximum percentage of ZC bond value that can be borrowed | 80% |
| Liquidation Threshold | Utilization ratio at which liquidation is triggered | 80% |
| Liquidation Amount | Maximum portion of obligation that can be liquidated | 50% |
| Liquidation Fee | Additional fee applied to liquidated amount | 7% (5% to liquidator, 2% to reserve) |
| Post-Liquidation Target | Target utilization ratio after liquidation | ~70% |

## Related Resources

- [ZC Bond Collateral](README.md)
- [Collateralization](../../../core-mechanics/collateralization.md)
- [Liquidation Process](../../../core-mechanics/liquidation/README.md)
- [Zero-Coupon Standard](../../../core-mechanics/standardization/zero-coupon-bonds.md)
