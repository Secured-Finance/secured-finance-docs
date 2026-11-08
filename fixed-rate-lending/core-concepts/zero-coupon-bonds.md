---
description: >-
  The instrument behind every fixed rate — price, discount factor, and APR in
  one page
---

# 💠 Zero-Coupon Bonds

A **Zero-Coupon (ZC) bond** pays no periodic interest. The difference between its purchase price and face value determines its rate for the term. Secured Finance quotes bond prices against a par value of **100**. Here, face value is the position’s maturity accounting value: at maturity the position **auto-rolls**, rather than automatically paying funds to your wallet. Review [Fixed Maturity & Auto-Roll](fixed-maturity-and-auto-roll.md) for the rollover rate and fees.

The discount-to-par structure makes term rates comparable without periodic coupon payments. Closing the position requires an executed unwind or offsetting trade against available liquidity, followed by a separate withdrawal.

## Price, discount factor, and value

The bond price _is_ the discount factor, scaled by 100:

$$
\text{ZC Bond Price} = \text{Discount Factor} \times 100
$$

For an executed amount at a given price, the gross relationship before fees is:

$$
FV = PV \times \frac{100}{\text{Bond Price}}
$$

**Example, excluding fees:** a fully executed purchase of 1,000 USDC face value at 96.90 costs 969 USDC (PV). The 31 USDC difference represents about **3.20% over the term**, not an annual rate. Actual proceeds depend on fees and how and when the position is closed.

**What to enter in the app:** the order **Amount** is PV in the selected currency. For example, an amount of 100 USDC fully executed at a price of 98 corresponds to approximately **102.0408 USDC FV** before fees and rounding (100 × 100 ÷ 98). Entering 100 USDC does not mean exactly 100 USDC of maturity value. Market orders can execute at several prices or fill only partly, so verify actual filled amounts and the resulting position.

## Converting price to APR

Trades execute on **price**; the app displays the implied **APR** as a reference, using the Act/365 day-count convention.

**Maturities under 1 year** (linear):

$$
APR = \left(\frac{100}{\text{Bond Price}} - 1\right)\times\frac{\text{seconds per year}}{\text{seconds to maturity}}
$$

**Example:** a bond with 90 days remaining at 98.50 → (100/98.50 − 1) × (365/90) ≈ **6.18% APR**, before fees.

**Maturities over 1 year** (annual compounding):

$$
APR = \left(\frac{100}{\text{Bond Price}}\right)^{1/\text{years to maturity}} - 1
$$

_Example:_ an 18-month bond at 85.00 → (100/85)^(1/1.5) − 1 ≈ **11.44% APR**.

{% hint style="info" %}
**Pre-open markets:** during the 7-day [Itayose](../advanced-topics/itayose.md) window, the displayed APR uses the _estimated opening price_ and measures time from the trading start date (not the current date) to maturity.
{% endhint %}

## Price bounds

Orders are capped at a price of **100.00** — the protocol does not allow negative yields. Prices are quoted to 2 decimal places. Per-block price movement is bounded by the [Circuit Breaker](../advanced-topics/circuit-breaker.md).

## Buying and selling in practice

* **Lend = buy the bond.** The execution price fixes the gross rate for the current term. Fees and the price at which you exit affect the realized return.
* **Borrow = sell the bond.** Execution credits funds to your protocol balance and creates an FV debt position. It requires [collateral](collateral.md); maturity does not automatically repay the debt.
* **To exit**, use Unwind or execute an opposite order in the same currency and maturity. Liquidity and permitted prices can limit execution to part or none of the position. Rates and fees may have moved against you; verify the remaining position after each attempt.
* **At maturity** the position [auto-rolls](fixed-maturity-and-auto-roll.md) at a new rate with a roll fee. To receive available assets in your wallet, close the intended exposure and then withdraw.

## Common questions

<details>

<summary>Why use ZC bonds instead of interest-bearing loans?</summary>

There are no periodic coupon payments to track. The discount-to-par structure makes rates for different maturities comparable, but it does not remove smart-contract risk, exit-liquidity risk, or the risk of a different rate at Auto-Roll.

</details>

<details>

<summary>How is my yield affected if I sell before maturity?</summary>

Your realized return depends on the execution price, filled amount and fees. A fall in rates generally raises bond prices, while a rise lowers them. An early exit can realize a loss, and available liquidity may prevent full closure.

</details>

<details>

<summary>Where can I see the exact math used by the contracts?</summary>

The contracts compute durations in seconds (seconds-per-year = 31,536,000). See the [Developer Portal](../../developer-portal/introduction.md) for SDK and subgraph access to raw prices.

</details>

## Related

* [Order Book & Order Types](order-book.md) — how bonds actually trade
* [APR vs APY](../advanced-topics/apr-vs-apy.md) — why we quote APR
* [Tokenization](tokenization.md) — ZC bonds as ERC-20 tokens
