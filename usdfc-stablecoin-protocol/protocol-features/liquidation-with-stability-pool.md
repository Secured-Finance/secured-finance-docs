---
description: Debt Repayment via Stability Pool
---

# 🏄 Liquidation with Stability Pool

## **What is the Stability Pool?**

The **Stability Pool** is a reserve of **USDFC** dedicated to absorbing liquidations when a borrower's collateral ratio falls below the required **110%**. The pool is used solely for liquidations, ensuring that under-collateralized positions can be settled and the system remains stable.

### **How the Stability Pool Works**

* **Purpose**: The Stability Pool repays the debt of liquidated borrowers using the deposited USDFC.
* **Depositor Rewards**: When USDFC from the pool is used, depositors receive **Filecoin (FIL)** from the liquidated collateral at a discount.

## **What are Liquidations?**

Liquidations occur when a Trove’s collateral ratio falls below **110%**, ensuring that all USDFC remains fully collateralized. In liquidation, the Stability Pool covers the Trove's debt, and its collateral is distributed to Stability Pool depositors. The Trove owner keeps their borrowed USDFC but loses collateral, typically incurring around a **10% loss**. To avoid liquidation, maintaining a collateral ratio of **150% or higher** is recommended.

### **Liquidation Process**

1. **Triggering Liquidation**: When a Trove’s collateral ratio falls below 110%, a **Liquidator** triggers the liquidation.
2. **Debt Repayment**: The Stability Pool covers the Trove’s debt by burning the corresponding amount of USDFC.
3. **Collateral Distribution**: The collateral (FIL) from the liquidated Trove is distributed to the Stability Pool depositors based on their pool share, minus the Liquidator’s compensation.

### **Role of the Liquidator**

* The **Liquidator** is responsible for triggering the liquidation process.
* As a reward, the Liquidator receives:
  * The **Liquidation Reserve** (a 20 USDFC reserve set aside during minting to cover gas fees).
  * **0.5%** of the liquidated collateral (FIL), incentivizing them to initiate liquidations.

### **Stakeholders in the Liquidation Process**

1. **Stability Pool Depositors**: Provide USDFC to the pool and receive FIL at a discount when liquidations occur. (Buy FIL Cheaper)
2. **Liquidated Borrowers**: Have their Trove liquidated when their collateral ratio falls below 110%, losing a portion of their collateral to repay their debt. Trove will be closed. (Sell FIL Cheaper)
3. **Liquidators**: Trigger the liquidation and receive gas compensation (Liquidation Reserve of 20 USDFC) plus 0.5% of the liquidated collateral.

***

## Price Oracle&#x20;

Secured Finance uses **Pyth** as the primary oracle to determine the **FIL** price. Pyth provides accurate and reliable real-time price feeds essential for system operations.

### **Fallback Mechanism**

In case of extreme conditions where the Pyth price feed is unavailable, the protocol switches to **Tellor** as a backup:

* **Pyth price not updated for over 4 hours**.
* **Pyth response reverts**, returns invalid data, or shows an invalid timestamp.
* **Price change between consecutive updates exceeds 50%**.

This dual-oracle approach ensures that the protocol maintains accurate pricing and stability, even under extreme conditions.

***

## **What Happens If the Stability Pool Is Empty?**

If the **Stability Pool** is empty during a liquidation, the protocol switches to a **redistribution mechanism**. In this case, the debt and collateral from the liquidated Trove are redistributed proportionally to all other existing Troves, based on their collateral amount.

#### Example of Redistribution

1. **Trove Liquidation**: A Trove is liquidated, but the Stability Pool has insufficient USDFC.
2. **Debt and Collateral Redistribution**: The debt and collateral are proportionally distributed to other active Troves.
3. **Impact on Troves**: Troves receiving the redistributed collateral and debt may see their collateral ratio lower, while the net USD value increase.&#x20;
