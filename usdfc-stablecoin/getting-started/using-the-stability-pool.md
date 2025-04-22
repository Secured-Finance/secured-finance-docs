---
description: Learn how to deposit USDFC into the Stability Pool and earn rewards
---

# 🏊 Using the Stability Pool

## Prerequisites
- USDFC tokens in your wallet
- Access to the [USDFC application](https://usdfc.secured.finance/)
- Connected wallet with enough FIL for gas fees

## Overview
The Stability Pool is a key component of the USDFC protocol that helps maintain system stability. By depositing your USDFC into the Stability Pool, you contribute to the liquidation mechanism and earn rewards in the form of liquidated FIL collateral. This guide will walk you through the process of depositing USDFC into the Stability Pool and understanding how rewards work.

## Step 1: Access the Stability Pool
First, you need to navigate to the Stability Pool section in the USDFC application.

1. Navigate to the [USDFC application](https://usdfc.secured.finance/)
2. Connect your wallet if not already connected
3. Locate and click on the "Stability Pool" option in the navigation menu

[Image: Screenshot of the USDFC application with the Stability Pool option highlighted]

## Step 2: Review Stability Pool Information
Before depositing, review the current Stability Pool information.

1. Check the total USDFC deposited in the Stability Pool
2. Review the current rewards and APR (if displayed)
3. Understand the liquidation history and potential future rewards

[Image: Screenshot of the Stability Pool dashboard showing key metrics]

## Step 3: Deposit USDFC
Now you can deposit your USDFC into the Stability Pool.

1. Enter the amount of USDFC you want to deposit
2. Review any fees or conditions associated with the deposit
3. Click the "Deposit" button
4. Confirm the transaction in your wallet
5. Wait for the transaction to be processed on the blockchain

[Image: Screenshot of the deposit interface with amount input field and deposit button]

## Step 4: Monitor Your Deposit and Rewards
After depositing, you can monitor your position and earned rewards.

1. Your deposit amount will be displayed in the Stability Pool dashboard
2. Any earned FIL rewards will accumulate over time
3. The dashboard will show your share of the Stability Pool and estimated rewards

[Image: Screenshot showing deposit and rewards information]

## Step 5: Claim Rewards (When Available)
When you've earned rewards, you can claim them.

1. Locate the "Claim Rewards" or similar button in the Stability Pool dashboard
2. Click the button to claim your earned FIL rewards
3. Confirm the transaction in your wallet
4. Wait for the transaction to be processed
5. Verify that the FIL rewards have been added to your wallet

[Image: Screenshot highlighting the claim rewards functionality]

## Step 6: Withdraw USDFC (When Desired)
You can withdraw your USDFC from the Stability Pool at any time.

1. Enter the amount of USDFC you want to withdraw
2. Click the "Withdraw" button
3. Confirm the transaction in your wallet
4. Wait for the transaction to be processed
5. Verify that the USDFC has been returned to your wallet

[Image: Screenshot of the withdrawal interface]

## How Stability Pool Rewards Work

### Liquidation Process
When a Trove is liquidated, the following happens:
1. The system identifies Troves with collateral ratios below the minimum requirement
2. USDFC from the Stability Pool is used to repay the debt of the liquidated Trove
3. The liquidated Trove's collateral is distributed to Stability Pool depositors proportionally

### Reward Distribution
Rewards are distributed based on your share of the Stability Pool:

$$
\text{Your Reward} = \text{Liquidated Collateral} \times \frac{\text{Your Deposit}}{\text{Total Stability Pool}}
$$

[Image: Visual representation of the reward distribution mechanism]

### Deposit Dilution
It's important to understand that your deposit may be "diluted" over time:
1. When liquidations occur, some of your deposited USDFC is used to repay debt
2. Your deposit amount decreases, but you receive FIL collateral in return
3. This is not a loss but a conversion from USDFC to FIL at a potentially favorable rate

[Image: Diagram explaining deposit dilution during liquidations]

## Strategies for Stability Pool Participation

### Conservative Strategy
- Deposit a small portion of your USDFC (10-20%)
- Lower risk and lower potential rewards
- Good for those who want to maintain liquidity

### Balanced Strategy
- Deposit a moderate portion of your USDFC (30-60%)
- Balance between liquidity and potential rewards
- Monitor the system health regularly

### Aggressive Strategy
- Deposit a large portion of your USDFC (70-100%)
- Higher potential rewards during periods of liquidations
- Less liquidity for other opportunities

[Image: Comparison chart of different Stability Pool strategies]

## Next Steps
- Learn about [redeeming USDFC](./redeeming-usdfc.md) when you're ready to exit
- Understand [Recovery Mode](../advanced-topics/recovery-mode.md) and how it affects the Stability Pool
- Explore other ways to use your USDFC in the ecosystem

## Troubleshooting
- **Transaction Failed**: Ensure you have enough FIL for gas fees
- **Cannot Deposit**: Verify that you have the USDFC amount you're trying to deposit
- **Rewards Not Showing**: Rewards only accumulate when liquidations occur; there may not have been recent liquidations

## Common Questions
**Q: Is there a minimum amount I need to deposit?**  
A: There is typically no minimum amount, but very small deposits may result in gas fees outweighing potential rewards.

**Q: How often are rewards distributed?**  
A: Rewards are distributed automatically during liquidation events. The frequency depends on market conditions and system health.

**Q: Can I lose my deposited USDFC?**  
A: Your deposit is used to repay liquidated debt, but you receive FIL collateral in return, often at a discount to market value.

**Q: How do I know if the Stability Pool is profitable?**  
A: Monitor the liquidation history and current system health. More liquidations generally mean more rewards for depositors.

## Related Topics
- [Liquidation](../core-mechanics/liquidation/)
- [Recovery Mode](../advanced-topics/recovery-mode.md)
- [Protocol Fees](../core-mechanics/protocol-fees.md)
- [The Trove System](../core-mechanics/the-trove-system.md)
