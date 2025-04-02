---
description: Understanding Debt Calculations and Required Amount Conditions
---

# ✏️ Trove Management

This chapter provides a detailed overview of Trove operations within the Secured Finance Stablecoin Protocol. You’ll learn how to open and close Troves, how liquidations work, how Recovery Mode changes certain calculations, and the significance of important parameters like the Borrowed Amount, Liquidation Reserve, Borrowing Fee, and Collateral Ratio.

***

## 1. Key Concepts and Definitions

### 1.1 Trove

A **Trove** is your personal vault within the protocol where you lock up Filecoin (FIL) as collateral in order to borrow USDFC. Each Trove tracks:

* The amount of collateral you have deposited (in FIL).
* Your **Total Debt** (in USDFC), which includes your Borrowed Amount, the Liquidation Reserve, and any applicable Borrowing Fee.

If your Collateral Ratio becomes lower than specific threshold, your Trove may be liquidated.

### 1.2 Borrowed Amount

The **Borrowed Amount** is how much USDFC you borrow when opening (or adjusting) a Trove.

* There is a **minimum borrow amount** of **180 USDFC**.

### 1.3 Liquidation Reserve

An amount of USDFC (currently **20 USDFC**) added to your Debt to cover gas costs if your Trove is liquidated.

* Refunded when you close your Trove.

### 1.4 Borrowing Fee (Minting Fee)

A **one-time fee** based on your Borrowed Amount:

$$
\text{Borrowing Fee} = (\text{Borrowed Amount}) \times (\text{Fee Rate})
$$

* **Deducted** from the borrowed USDFC.
* **Fee Rate** can vary from **0.5%** to **5%**.
* **Waived** in Recovery Mode.
* No recurring interest is charged (it’s just this one-time fee).

### 1.5 Total Debt

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve}) + (\text{Borrowing Fee})
$$

You must repay this (minus the Liquidation Reserve that’s refunded) to reclaim all your collateral.

### 1.6 Collateral Ratio

$$
\text{Collateral Ratio} = \frac{\text{Collateral Value (USD)}}{\text{Total Debt (USDFC)}}
$$

* **Minimum:** 110% (Normal Mode).
* **Recommend >150%** to avoid liquidation in Recovery Mode; many users keep 200–250% as an extra buffer.

***

## 2. Action-Specific Debt Calculations

### 2.1 Opening a Trove

* **Normal Mode**

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve}) + (\text{Borrowing Fee})
$$

*   **Recovery Mode**

    Borrowing Fee is waived

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve})
$$

**Example (Normal Mode)**

* Borrowed Amount: 180 USDFC
* Liquidation Reserve: 20 USDFC
* Borrowing Fee: 0.90 USDFC (0.5% of 180)
* **Total Debt:** 200.90 USDFC

***

### 2.2 Liquidation (Risky Troves)

If your Collateral Ratio is too low, your Trove can be liquidated. **No additional fee** applies at liquidation, but you risk losing collateral.

1. **Normal Mode**
   * Collateral Ratio below 110% ⇒ subject to liquidation.
   * You effectively swap your collateral for the borrowed USDFC.
2. **Recovery Mode**
   * Triggered if the system’s Total Collateral Ratio (TCR) < 150% (for example).
   * Troves below that TCR can be liquidated.
   * Up to **110%** of your Debt (in collateral value) can be seized; the remainder stays with you.

***

### 2.3 Closing a Trove

To close your Trove, you must repay your **Total Debt**. However, because the protocol immediately refunds the 20 USDFC Liquidation Reserve, you only need to **prepare** the net amount (i.e., Total Debt – Reserve).

**Example:**

* Borrowed Amount: 180 USDFC
* Liquidation Reserve: 20 USDFC
* Borrowing Fee: 0.90 USDFC
* **Total Debt:** 200.90 USDFC
* **Amount You Need to Prepare:** 200.90 – 20 = **180.90 USDFC** (because the 20 USDFC reserve is automatically offset and returned).

Hence, your actual out-of-pocket requirement is 180.90 USDFC to close the Trove.

***

## 3. Additional Notes

* **Interest-Free Borrowing:** Only a one-time Borrowing Fee applies (no ongoing interest).
* **Monitor Collateral Ratio:** Aim above 150% to reduce liquidation risk, especially in volatile markets.
* **Parameters May Vary:** Check the official docs for the latest [Fee Rates](protocol-fees.md) and Liquidation Reserve settings.

For more on redemptions (and how they support the USDFC peg), see the [Redemption as Peg Mechanism](https://docs.secured.finance/stablecoin-protocol-guide/key-features/redemption-as-peg-mechanism). Understanding these basics helps you manage your Trove effectively and protect your collateral.

o1
