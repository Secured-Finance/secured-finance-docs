---
description: The main feature to generate USDFC and borrow it into your connected wallet.
icon: pickaxe
---

# Mint & Borrow

{% hint style="success" %}
**Why Mint & Borrow USDFC?**

* Get instant and ample $ liquidity without selling FIL
* No need for counterparties or external exchanges
* Keep FIL securely in a trove while enhancing capital efficiency
{% endhint %}

## **How It Works**

To use USDFC, you first open a trove to manage your FIL collateral and USDFC debt, maintaining a **minimum collateralization ratio (MCR) of 110%** to avoid [liquidation](https://app.gitbook.com/o/DralddHerVJQe2eHzg9a/s/5n2yKWdxy0II5Sd3ZIQL/~/changes/185/stablecoin-protocol-guide/key-features/liquidation-with-stability-pool#what-are-liquidations). This ensures the safety and stability of the system. The process involves the following steps:

1. **Deposit FIL as Collateral**
   * Prepare FIL in your wallet to cover the USDFC debt (borrowed amount + mint fees)
   * Open a trove and input a FIL amount to deposit as collateral.
   * Input USDFC amount you want to borrow (after minted inside your trove)
     * You must maintain at least a 110% collateral ratio.
2. **Mint USDFC**
   * Once the FIL amount and USDFC amount is set, check that the [minting costs](https://app.gitbook.com/o/DralddHerVJQe2eHzg9a/s/5n2yKWdxy0II5Sd3ZIQL/~/changes/185/stablecoin-protocol-guide/key-features/mint-and-borrow#minting-costs) is added as total debt, then you can click confirm.
   * Your connected wallet (ex. MetaMask) asks you to send a transaction.
   * Once the USDFC amount is minted, you can see your borrowed amount in the app.
   * Please import the USDFC contract [address](../deployed-contracts.md#contract-addresses) to your wallet so you can use it anywhere.
3. **Maintain Collateral Ratio**
   * The minimum collateralization ration (MCR) is set to 110%.
     * For instance, if you deposit 1,000 USD worth of FIL, you can mint up to 909 USDFC, keeping a 110% collateral ratio.
   * It’s crucial to monitor your collateral ratio to avoid liquidation. If the collateral value drops, consider adding more FIL or repaying some USDFC to maintain a healthy buffer.
4. **Adjust or Close**
   * You can make adjustments on your trove to manage FIL collateral and USDFC debt.
   * Adjustment is used to add/reduce collateral, or borrow/repay USDFC.
   * If you no longer need the trove, you can close it by repaying debts (borrowed + fees) in USDFC.
     * You don't need to repay the liquidation reserve.
5. **3rd Party Trove Adjustment (Liquidation & Redemption)**
   * You should be aware that your trove can be adjusted by special conditions below.
   * To protect the system, anyone can liquidate your collateral using USDFC stability pool for the trove below 110% collateral ratio.
   * To ensure 1:1 peg, anyone can bring USDFC and redeem FIL collateral for the trove with the lowest collateral ratio.

{% hint style="warning" %}
The system requires to keep a minimum borrowed amount of 180 USDFC and reserves an additional 20 USDFC as long as trove exists. It creates limitations on all trove activities.
{% endhint %}

{% hint style="warning" %}
When you want to close your trove completely, you should repay borrowed amount + minting fees in USDFC.
{% endhint %}

## **Minting Costs**

When you mint USDFC, the following costs apply:

$$\text{Minting Fee} =  \text{Liquidation Reserve} + \text{One-Time Minting Fee}$$

### **1. Liquidation Reserve**:

* A **20 USDFC reserve** is added to your debt when minting USDFC. This reserve is intended to cover gas fees in case of liquidation.
* If no liquidation occurs and you fully repay your debt, the **20 USDFC reserve** will be refunded when you close your position.
* When you close your trove completely, the reserve will be returned and burnt.

### **2. One-Time Minting Fees**:

$$\text{One-Time Minting Fee} = (\text{Base Rate} + 0.5\%) \times \text{Minted USDFC}$$

* The **Minting (Borrowing) Fee** consists of two parts:
  * **Fixed Fee (0.5%)**:  Fixed fee charged at the time of minting.
  * **Base Rate (0% to 4.5%)**: The [Base Rate](https://app.gitbook.com/o/DralddHerVJQe2eHzg9a/s/5n2yKWdxy0II5Sd3ZIQL/~/changes/185/stablecoin-protocol-guide/key-features/mint-and-borrow#base-rate-explanation) varies depending on the system’s conditions.&#x20;
* Together, the Minting Fee ranges from **0.5% to 5%**, making it a one-time cost and added to your debt.
* During **Recovery Mode**, the Minting Fee is set to **0%**, encouraging users to add collateral and stabilize the system.

### **Total Debt Calculation Example**

$$\text{Total Debt = Borrowed amount + Liquidation Reserve + One-Time Minting Fees}$$

* If you mint **4,000 USDFC** with a **Base Rate** of **0.5%**:
* **Liquidation Reserve**: 20 USDFC.
* **One-Time Minting Fee**: Fixed Fee + Base Rate = 40 USDFC.
  * **Fixed Fee**: 0.5% of 4,000 USDFC = 20 USDFC.
  * **Base Rate**: 0.5% of 4,000 USDFC = 20 USDFC (usually 0%).
* **Total Debt**: 4,060 USDFC.

***

**0% Interest Rate Fee:**

At the current stage, Secured Finance does not charge any ongoing **interest rate fees** on USDFC. This strategic decision allows for a more accessible and user-friendly experience:

{% hint style="info" %}
**Why no interest fees?**

* Our primary goal is to foster the **widespread adoption of USDFC** within the Filecoin ecosystem and make it more attractive for DeFi users.
* By keeping the **interest rate at 0%**, we are encouraging users to mint and use USDFC without the added burden of accumulating interest over time.&#x20;

We may introduce an **interest rate fee** on borrowed USDFC in the future to further support the long-term sustainability of the protocol
{% endhint %}

***

## **Base Rate Explanation**

The **Base Rate** is a dynamic component of the borrowing fee that adjusts according to market conditions and redemption activity:

### **Dynamic Range**:

* The Base Rate ranges from **0% to 4.5%**, adjusting based on the amount of USDFC redeemed relative to the total USDFC supply.
* The full Minting and Redemption Fee (fixed fee + base rate) therefore ranges between **0.5% and 5%**.

### **Calculation**:

The Base Rate is initially set at **0%** and adjusts based on the redemption activity. The formula for updating the Base Rate is:

$$
\text{Base Rate}_t = \text{Base Rate}_{t-1} + 0.5 \times \left( \frac{m}{n} \right)
$$

Where:\
m = amount of USDFC redeemed\
n = current total supply of USDFC

### **Decay**:

The Base Rate decays over time when there is low redemption activity, following a **12-hour half-life**. This ensures that the Base Rate gradually returns to its baseline if no significant redemption activity occurs.

The decay formula is:

$$
\text{Base Rate}_t = \text{Base Rate}_{t-1} \times \delta^{\Delta t}
$$

Where:\
δ = hourly decay factor (e.g., 0.944)\
Δt = time elapsed (in hours) since the last redemption or loan issuance.



{% hint style="info" %}
The decay factor `δ` (0.944) is selected to ensure a 12-hour half-life for the base rate.
{% endhint %}

### **Purpose**:

The Base Rate is designed to maintain stability in the USDFC supply by adapting to market conditions. It helps regulate borrowing behavior, balancing liquidity and redemption activity while keeping the system solvent.
