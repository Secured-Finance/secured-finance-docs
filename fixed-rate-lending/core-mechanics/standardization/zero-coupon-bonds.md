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

> **Example**: Consider an example where Bob lends 1,000 FIL for 1 year at 80.00 through our platform. At maturity, he will receive 1,250 FIL, which is calculated as 1,000 \* 100 / 80. The Annual Percentage Yield (APY) of this transaction is 25%, as Bob earned 250 FIL from his initial investment of 1,000 for 1 year.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Bond Par Value | The value at which bonds are redeemed at maturity | 100 |
| Maximum Bond Price | The maximum price allowed for bond orders | 100.00 |
| Minimum Bond Price | The minimum price allowed for bond orders | Varies by asset |
| Price Precision | Decimal precision for bond prices | 2 decimal places |
| Yield Calculation | How yield is calculated from bond price | See [ZC Bond Price to APR](../../advanced-topics/zc-bond-price-to-apr.md) |

{% hint style="info" %}
What is the price range of the Zero-Coupon bond?

Our platform enforces a strict constraint on the ZC bond price, capping orders at 100.00. This indicates that the protocol precludes negative yields on the corresponding assets, rendering them unfeasible for placement.
{% endhint %}

## Related Resources

- [Fixed Maturity](fixed-maturity.md)
- [Orderbook Mechanics](../order-book-system.md)
- [ZC Bond Price to APR](../../advanced-topics/zc-bond-price-to-apr.md)
- [Discount Factor](../../advanced-topics/discount-factor.md)
