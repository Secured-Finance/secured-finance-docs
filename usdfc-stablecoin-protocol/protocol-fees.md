# 🧀 Protocol Fees

The **Fee Reserve** is a dedicated pool where protocol fees are collected and stored. These accumulated fees are crucial for the protocol’s sustainability and will eventually be distributed to **the Secured Finance Token Stakers** following the **Token Generation Event (TGE)**.

The Fee Reserve is funded through various fees generated by user interactions with the protocol. Below is a breakdown of these fees and how they contribute to the Fee Reserve.

## **Fee Structure**

1. **Minting Fee**
   * The **Minting Fee** is charged whenever users mint **USDFC** by depositing collateral.
   * The fee is calculated as **(Base Rate + 0.5%)** applied to the minted amount of USDFC.
   * This fee is directed entirely to the Fee Reserve, ensuring that every minting transaction supports the protocol’s sustainability.
2. **Redemption Fee**
   * The **Redemption Fee** is applied when users redeem USDFC for **Filecoin (FIL)** at face value. This fee incentivizes stability within the protocol and provides a mechanism to bring USDFC back to its 1:1 USD peg when necessary.
   * The Redemption Fee is calculated as **(Base Rate + 0.5%)** of the redeemed USDFC amount.
   * Like the Minting Fee, all proceeds from the Redemption Fee are added to the Fee Reserve.
3. **Interest Fee**
   * **Interest Fee** is currently set to **0%**. This means that borrowers do not incur any recurring interest costs on their debt, encouraging wider adoption and utility of USDFC.
   * The zero-interest model is strategic, aiming to boost the initial circulation of USDFC within the Filecoin ecosystem. This parameter may be reconsidered in the future based on market conditions.

## **Post-TGE Distribution**

After the **Token Generation Event (TGE)**, the Fee Reserve will be redistributed back to the Secured Finance Token Stakers as a reward. This model aligns incentives, rewarding early supporters and active participants while maintaining the protocol's stability.

## **Summary of Fee Allocation**

<table><thead><tr><th width="192">Fee Type</th><th width="326">Calculation</th><th>Destination</th></tr></thead><tbody><tr><td><strong>Minting Fee</strong></td><td>(Base Rate + 0.5%) * Minted USDFC</td><td>Fee Reserve</td></tr><tr><td><strong>Redemption Fee</strong></td><td>(Base Rate + 0.5%) * Redeemed USDFC</td><td>Fee Reserve</td></tr><tr><td><strong>Interest Fee</strong></td><td>0%</td><td>N/A</td></tr></tbody></table>

