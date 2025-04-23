---
description: Understanding the core vault system for managing collateral and debt
---

# ✏️ The Trove System

## Overview

The Trove System is the foundation of the USDFC Stablecoin Protocol, providing users with personal vaults to deposit Filecoin (FIL) collateral and borrow USDFC. Each Trove tracks your collateral, debt, and maintains a collateralization ratio that must stay above the minimum threshold to avoid liquidation.

## How It Works

A Trove is your personal vault within the protocol where you lock up Filecoin (FIL) as collateral in order to borrow USDFC. The system carefully tracks the relationship between your collateral value and debt to ensure the protocol remains solvent.

### Key Components

1. **Collateral**: The amount of FIL you deposit to secure your borrowed USDFC
2. **Total Debt**: The sum of your borrowed USDFC, liquidation reserve, and any applicable fees
3. **Collateral Ratio**: The ratio of your collateral value (in USD) to your total debt (in USDFC)

### Trove Lifecycle

1. **Opening a Trove**: Deposit FIL collateral and specify how much USDFC to borrow
2. **Managing a Trove**: Add collateral or repay debt to maintain a healthy collateral ratio
3. **Closing a Trove**: Repay all debt to reclaim your collateral
4. **Liquidation**: If your collateral ratio falls below the minimum threshold, your Trove may be liquidated

## Key Parameters

| Parameter                | Description                                        | Default Value |
| ------------------------ | -------------------------------------------------- | ------------- |
| Minimum Collateral Ratio | Minimum required ratio in Normal Mode              | 110%          |
| Recovery Mode Threshold  | System-wide ratio that triggers Recovery Mode      | 150%          |
| Minimum Borrow Amount    | Minimum USDFC that can be borrowed                 | 180 USDFC     |
| Liquidation Reserve      | USDFC reserved for potential liquidation gas costs | 20 USDFC      |

## Debt Calculations

### Total Debt Formula

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve}) + (\text{Borrowing Fee})
$$

The Total Debt represents the full amount you owe to the protocol, including:

* **Borrowed Amount**: The USDFC you receive (minimum 180 USDFC)
* **Liquidation Reserve**: 20 USDFC set aside to cover potential liquidation costs (refunded when you close your Trove)
* **Borrowing Fee**: One-time fee based on your borrowed amount (waived in Recovery Mode)

### Collateral Ratio Formula

$$
\text{Collateral Ratio} = \frac{\text{Collateral Value (USD)}}{\text{Total Debt (USDFC)}}
$$

* Must remain above 110% in Normal Mode
* Recommended to maintain above 150% to avoid liquidation in Recovery Mode
* Many users maintain 200-250% as an extra safety buffer

## Action-Specific Calculations

### Opening a Trove

**Normal Mode**:

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve}) + (\text{Borrowing Fee})
$$

**Recovery Mode**:

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve})
$$

(Borrowing Fee is waived)

**Example (Normal Mode)**:

* Borrowed Amount: 180 USDFC
* Liquidation Reserve: 20 USDFC
* Borrowing Fee: 0.90 USDFC (0.5% of 180)
* **Total Debt**: 200.90 USDFC

### Closing a Trove

To close your Trove, you must repay your Total Debt. However, the protocol immediately refunds the Liquidation Reserve, so you only need to prepare the net amount.

**Example**:

* Total Debt: 200.90 USDFC
* Liquidation Reserve: 20 USDFC
* **Amount You Need to Prepare**: 180.90 USDFC

## Common Questions

**Is there any ongoing interest on my borrowed USDFC?**\
No, the protocol only charges a one-time Borrowing Fee when you mint USDFC. There are no recurring interest charges.

**What collateral ratio should I maintain to be safe?**\
While the minimum is 110%, it's recommended to maintain at least 150% to avoid liquidation during Recovery Mode. Many users maintain 200-250% as an extra safety buffer.

**What happens to my Liquidation Reserve?**\
The 20 USDFC Liquidation Reserve is automatically refunded when you close your Trove. If your Trove is liquidated, this reserve is used to compensate the liquidator for gas costs.

[Learn more in the FAQs section](../faqs.md)

## Related Topics

* [Mint & Borrow](mint-and-borrow.md)
* [Liquidation](liquidation.md)
* [Redemption](redemption.md)
* [Recovery Mode](../advanced-topics/recovery-mode.md)
