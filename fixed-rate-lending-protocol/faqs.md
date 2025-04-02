---
description: Answers to Frequently Asked Questions
---

# ❓ FAQs

{% tabs %}
{% tab title="Overview" %}
### What is Secured Finance?

Secured Finance is a decentralized finance platform that facilitates peer-to-contract lending and derivatives trading. It's built on the Ethereum blockchain, offering a transparent, robust, and cost-effective alternative to traditional financial institutions. For more details, you can refer to our Secured Finance [Overview](../) section.

### What products does Secured Finance offer?

Secured Finance's inaugural offering is the Loan Market Platform, designed to facilitate seamless peer-to-peer lending and derivatives trading for fixed-income investments and hedging. For more details, you can refer to our [Loan Market Platform](platform-navigation/) section.

### What is a Zero-Coupon Bond (ZC Bond)?

A Zero-Coupon Bond (ZC Bond) is a type of bond that does not pay interest (coupons) during its life. Instead, it is sold at a discount to its face value and pays the full face value at maturity. This makes them ideal for users who want a guaranteed return at a specific point in the future. For more details, you can refer to our [Zero-Coupon Bond](protocol-features/zero-coupon-standard/) section.

### How do I buy or sell a ZC Bond on Secured Finance?

To buy or sell a ZC Bond on Secured Finance, you can browse the orders on our platform's orderbook. Once you have found a contract you want to buy or sell, you can execute the transaction directly from the platform. The platform uses smart contracts to transfer ownership of the contract to you automatically and to ensure that payments are made as specified in the order. For a step-by-step guide, you can refer to our [User Guides](beginners-guide.md) section.

### **What is the underlying asset for zero-coupon bonds?**

A: The underlying asset for zero-coupon bonds is the specific digital asset lent by the user. For example, lending ETH in the "September 2026 Order Book" mints a bond called **"ZC ETH SEP2026"**, representing the loaned ETH and its maturity date.

### **Can zero-coupon bonds be used outside the Secured Finance platform?**

A: Yes, zero-coupon bonds are tokenized and fully transferable. They can be used on other DeFi protocols for trading, as collateral, or for yield optimization opportunities.
{% endtab %}

{% tab title="Trading" %}
### Is my money locked and need to wait until maturity?

No. There is **no lock-up period** involved. Similar to spot transactions, our platform facilitates the trading of Zero Coupon Bonds (ZC Bonds) anytime you like. It is available 24/7!

If you are a lender, meaning you hold a ZC Bond, you can access your funds by either unwinding or selling the ZC Bond any time. This process allows you to withdraw the funds. Similarly, if you have an open limit order that hasn't been executed, you can cancel the order to withdraw your funds.

### How does lending and borrowing work on Secured Finance?

On Secured Finance, lending and borrowing work through the creation and trading of ZC Bonds. If you want to borrow digital assets, you can create a ZC Bond order and sell it on the platform. If you want to lend digital assets, you can buy a ZC Bond from the platform. The platform uses smart contracts to ensure that the terms of the contract are automatically enforced. This means payments are automatically transferred when due. For more details, you can refer to our [OTC Lending](platform-navigation/trading/) section.

### **What is the user journey for lending assets?**

A: Users connect their wallet, deposit collateral, select an order book with a preferred maturity date, and lend assets. They receive zero-coupon bonds as proof of lending, which can be redeemed at maturity for the principal plus yield.

### What is the Itayose process?

The Itayose process is a matching algorithm used in financial markets to ensure fair and efficient order execution. It's a method used by Secured Finance to match orders when a new order book starts trading in a way that prioritizes the highest bid and lowest ask prices. For more details, you can refer to our [Itayose Process](protocol-features/new-market-listing-and-delisting/itayose-fair-price-discovery.md) section.

### What is Auto-Rolling?

Auto-Rolling is a feature on Secured Finance that allows for automatic reinvestment of funds at maturity. This feature helps mitigate reinvestment risk, ensures cost-efficiency, and promotes continuous growth for users. For more details, you can refer to our [Auto-Rolling](protocol-features/auto-rolling/) section.

### **What happens to my outstanding order when the order book matures?**

Your outstanding order will be sent to your Collateral Vault upon the maturity of the order book. From there, you can either use these funds to place new trades or choose to withdraw them from the vault.

### Why is My Unwinding order 'Blocked'? What does it mean by 'Partially Blocked'?

When unwinding an order, it may become **'Blocked'** if there are no matching orders available on the Orderbook to satisfy your request. This could occur for two main reasons: 1) The amount of available orders is less than the quantity you wish to unwind, or 2) Even if there is an order with a sufficient amount, it might be outside the price range set by our Circuit Breaker, thus preventing a match. In cases where only part of your unwinding order is executed and the rest remains unmatched, the status will be marked as **'Partially Blocked'**. In such instances, you may either wait for a matching order to appear or place a limit order on the Orderbook and wait for it to be executed. \
The Circuit Breaker is a safety feature implemented in our protocol to limit price deviations from the mark price, designed to prevent price manipulation. For more information, please refer to the relevant section on [Circuit Breakers](protocol-security-and-safety/circuit-breaker/).
{% endtab %}

{% tab title="Collateral" %}
### What is collateral and why is it needed?

Collateral is an asset that a borrower offers to Secured Finance's platform to secure a loan. If the borrower defaults on loan repayments, the lender can seize the collateral to recover their losses. On Secured Finance, collateral is needed to ensure the security and integrity of the lending and borrowing process. For more details, you can refer to our [Collateral](faqs.md#collateral) section.

### What types of assets can be used as collateral on Secured Finance?

Secured Finance currently accepts Wrapped BTC, ETH, USDC, FIL and iFIL (only on FVM) as collateral. These assets were chosen due to their stability and wide acceptance in cryptocurrency. However, Secured Finance is always exploring the addition of more assets to expand its offering.&#x20;

### What happens if the value of my collateral falls?

If the value of your collateral falls and the loan-to-value (LTV) ratio exceeds the specified limit, your position may be liquidated. This is to ensure the security of the loan for the lender. For more details, you can refer to our [Liquidation](protocol-features/liquidation/) section.
{% endtab %}
{% endtabs %}

