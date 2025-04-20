---
description: Understanding Zero-Coupon Bonds as the standardized instrument in the Fixed-Rate Lending Protocol
icon: 💠
---

# 💠 Zero-Coupon Standard

## Overview

Zero-Coupon bonds are debt securities that do not pay interest (coupons) but are traded at a deep discount, rendering profit at maturity when the bond is redeemed for its full face value. The Secured Finance platform uses Zero-Coupon bonds as the standardized instrument for fixed-rate lending and borrowing.

## What You'll Learn

- Why Zero-Coupon bonds were chosen as the standard for the Fixed-Rate Lending Protocol
- How Zero-Coupon bonds work in practice
- How to calculate returns from Zero-Coupon bond investments
- How the platform handles bond pricing and yield calculations
- What constraints are placed on Zero-Coupon bond prices

## How It Works

The Zero-Coupon standard was chosen for its cost efficiency, simplicity, and low risk. With only two cash flows involved in the transaction - the initial and final exchanges - it saves on gas and operational costs. Investors can enjoy the simplicity of not having to track or reinvest coupon payments. The frequency of transactions is minimized, reducing operational risks.

Zero-Coupon bonds are traded at a discount to their face value and redeemed at full face value at maturity. On the Secured Finance platform, bonds are redeemable at 100.

The platform streamlines the borrowing and lending process by allowing users to specify the desired 'Price' and 'Amount' parameters. The system instantaneously calculates the implied Annual Percentage Rate (APR), interest accrual, estimated $ value, and transaction fee upon submission. For further information on [ZC Bond Price to Yield conversion](../../advanced-topics/zc-bond-price-to-apr.md), please consult the relevant materials.

## Examples

### Example 1: Lending with Zero-Coupon Bonds

Bob wants to lend 1,000 FIL for 1 year at a 25% APY:

1. He navigates to the lending interface and selects the 1-year maturity market
2. For a 25% APY, he sets his price at 80.00 (calculated as: 100 / (1 + 0.25) = 80)
3. He places a limit order to buy Zero-Coupon bonds at this price
4. When the order is filled, he pays 800 FIL (1,000 × 80.00 / 100)
5. At maturity, he receives 1,000 FIL, earning 200 FIL in interest
6. This represents a 25% return on his initial investment of 800 FIL

### Example 2: Borrowing with Zero-Coupon Bonds

Alice needs to borrow FIL for 6 months and is willing to pay a 20% APR:

1. After depositing sufficient collateral, she navigates to the borrowing interface
2. For a 20% APR on a 6-month term, the price would be approximately 90.91
   (calculated as: 100 / (1 + 0.20 × 0.5) = 90.91)
3. She places a market order to sell Zero-Coupon bonds at this price
4. When the order is filled, she receives 909.1 FIL upfront (1,000 × 90.91 / 100)
5. At maturity, she will need to repay 1,000 FIL
6. The effective interest paid is 90.9 FIL on a loan of 909.1 FIL for 6 months

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Bond Par Value | The value at which bonds are redeemed at maturity | 100 |
| Maximum Bond Price | The maximum price allowed for bond orders | 100.00 |
| Minimum Bond Price | The minimum price allowed for bond orders | Varies by asset |
| Price Precision | Decimal precision for bond prices | 2 decimal places |
| Yield Calculation | How yield is calculated from bond price | See [ZC Bond Price to APR](../../advanced-topics/zc-bond-price-to-apr.md) |

## FAQ

### Why use Zero-Coupon bonds instead of traditional interest-bearing loans?

Zero-Coupon bonds offer several advantages: they're simpler to implement on-chain (only two cash flows), more gas-efficient, eliminate reinvestment risk for lenders, and provide clear, upfront terms for both borrowers and lenders. The discount-to-par structure also makes yield calculations transparent and intuitive.

### How do I calculate the yield on a Zero-Coupon bond?

For bonds with maturity less than 1 year:
APR = (100/BondPrice - 1) × (365/DaysToMaturity)

For bonds with maturity greater than 1 year:
APR = (100/BondPrice)^(1/YearsToMaturity) - 1

### Can I sell my Zero-Coupon bond before maturity?

Yes, you can sell your position before maturity by taking an opposite position in the market. For example, if you initially lent (bought bonds), you can exit early by borrowing (selling bonds) of the same maturity. This effectively closes your position, though market conditions at the time will determine whether you realize a gain or loss.

### What happens at bond maturity?

At maturity, Zero-Coupon bonds are automatically redeemed at their par value (100). Lenders receive the full face value of their bonds, and borrowers must have sufficient funds to cover their repayment obligations. The protocol handles this settlement process automatically.

{% hint style="info" %}
What is the price range of the Zero-Coupon bond?

Our platform enforces a strict constraint on the ZC bond price, capping orders at 100.00. This indicates that the protocol precludes negative yields on the corresponding assets, rendering them unfeasible for placement.
{% endhint %}

## Related Resources

- [Fixed Maturity](fixed-maturity.md)
- [Orderbook Mechanics](../order-book-system.md)
- [ZC Bond Price to APR](../../advanced-topics/zc-bond-price-to-apr.md)
- [Discount Factor](../../advanced-topics/discount-factor.md)
