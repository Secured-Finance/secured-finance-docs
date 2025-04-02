---
description: Unpacking the Liquidation Process
---

# 🚰 Liquidation

## Why Liquidation process is important?

The liquidation process holds paramount importance for Secured Finance as a Decentralized Loan Protocol, primarily for two crucial reasons:

1. **Mitigating default risk:** Through the liquidation process, lenders are safeguarded against the risk of default by borrowers. When a borrower's collateral value falls below the liquidation threshold, their loan becomes eligible for liquidation, ensuring the lenders can recover their funds.
2. **Maintaining protocol stability:** The liquidation process plays a pivotal role in preserving the stability of the DeFi loan protocol. It prevents the accumulation of undercollateralized loans. Excessive loan defaults can deplete the protocol's reserves, potentially leading to system instability. By executing liquidations, the protocol can maintain a healthy balance and ensure its overall stability.

## How does it work?

When the borrower's [**Loan to Value**](./#loan-to-value) ratio surpasses the [**Threshold**](./#threshold)**,** the borrower's asset will be subject to liquidation.

During a liquidation process, a portion of the borrower's outstanding debt, which can be up to 50%, is repaid using the available collateral. The amount repaid from the debt is equal to the sum of the [**Collateral**](../../platform-navigation/portfolio/collateral-management.md) used for repayment and the [**Liquidation Penalty**](./#liquidation-penalty).

#### Loan to Value

The ratio of the borrower's debt to the collateral, also known as Loan to Value (LTV), indicates the buffer available until liquidation. The platform displays this ratio in the image below, where Green represents low risk, Yellow indicates moderate risk, and Red signifies high risk on the portfolio management tab.\


<figure><img src="../../../.gitbook/assets/risk-v2.gif" alt="" width="563"><figcaption><p>LTV and Liquidation Risk</p></figcaption></figure>

#### Threshold

The liquidation threshold for all currencies in our protocol is currently set at 80%. However, we continuously assess and adjust this ratio based on market conditions, taking into account factors such as the volatility and liquidity of each digital asset. It is imperative for each borrower to be initially over-collateralized to ensure the security and stability of the lending process.

#### Price Oracle

We use an on-chain live calculation based on the chainlink price feed for the collateral value.

## Liquidation Penalty

Our protocol charges a 7% liquidation penalty for the liquidated asset. Borrowers need to manage their collateral carefully to avoid the extra cost. This [fee](../../protocol-fees.md) is paid to the liquidation agent and reserve fund to secure the protocol.&#x20;

> See more details at [Liquidation Case study](case-study.md)

##
