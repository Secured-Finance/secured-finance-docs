---
description: Decoding Key Concepts
---

# 🧩 On-Chain Orderbook System

Secured Finance's Loan Market Platform incorporates an on-chain orderbook system, a pioneering application in the DeFi space. This system facilitates the trading of [Zero-Coupon bonds](zero-coupon-standard/) with a specific maturity date. To ensure clarity, we've defined some key terms used on our platform:

## **What is an Orderbook?**&#x20;

It is an electronic list of buy and sell orders for Zero-Coupon bonds, organized by price level. It enhances transparency by providing visualized information on price, availability, depth of trade, and more.

## **What is a Borrow Order?**

It refers to an order to borrow crypto assets, equivalent to selling a bond on our platform. After pledging sufficient collateral, you can place a sell order, selling a Zero-Coupon bond and receiving the equivalent cash upfront. You then owe the obligation to repay the money with interest at maturity.

## **What is a Lend Order?**

This is an order to lend, equivalent to buying a bond. You buy a Zero-Coupon bond at a discount, which will be redeemable at par at expiration.

## **What is a** [**Zero-Coupon Bond (ZC bond)**](zero-coupon-standard/)**?**

A Zero-Coupon bond is a debt security that doesn't pay interest (coupons) but is traded at a deep discount, rendering profit at maturity when the bond is redeemed for its full face value. On our platform, bonds will be redeemable at 100.



{% hint style="info" %}
**Why is On-Chain Orderbook so difficult?**

The on-chain Orderbook system is often perceived as inefficient due to high gas costs. As a result, many DeFi projects rely on the liquidity pool system (LP) which is a great financial innovation for gathering liquidity. However, the interest rate provided by the pool lacks composability and transparency. Secured Finance has successfully deployed an on-chain orderbook system using the 'lazy evaluation' method, which significantly reduces gas costs. Learn more details at '[Full On-Chain Orderbook system](../on-chain-orderbook-deep-dive/)' at technical overview.
{% endhint %}

