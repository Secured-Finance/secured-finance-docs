---
description: >-
  The instrument behind every fixed rate — price, discount factor, and APR in
  one page
---

# 💠 Zero-Coupon Bonds

A **Zero-Coupon (ZC) bond** pays no periodic interest. It trades at a discount and is redeemed at its full face value at maturity — the discount _is_ the interest. On Secured Finance, every ZC bond has a face value (par) of **100**, so a bond's price directly expresses its market-implied rate.

The ZC structure was chosen deliberately: only two cash flows (entry and maturity) means minimal gas, no coupon tracking or reinvestment, and transparent yield math.

## Price, discount factor, and value

The bond price _is_ the discount factor, scaled by 100:

$$
\text{ZC Bond Price} = \text{Discount Factor} \times 100
$$

From any position you can compute present and future value:

$$
FV = PV \times \frac{100}{\text{Bond Price}}
$$

**Example:** Bob buys 1,000 FIL notional of a ZC bond at 96.90. He pays 969 FIL today (PV) and holds a claim worth 1,000 FIL at maturity (FV) — a 3.2% return over the term, fixed at execution.

## Converting price to APR

Trades execute on **price**; the app displays the implied **APR** as a reference, using the Act/365 day-count convention.

**Maturities under 1 year** (linear):

$$
APR = \left(\frac{100}{\text{Bond Price}} - 1\right)\times\frac{\text{seconds per year}}{\text{seconds to maturity}}
$$

_Example:_ a 3-month bond at 98.50 → (100/98.50 − 1) × 4.055 ≈ **6.17% APR**.

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

* **Lend = buy the bond.** Your yield is locked if you hold to maturity.
* **Borrow = sell the bond.** You receive the discounted amount now and owe 100 per bond at maturity. Requires [collateral](collateral.md).
* **Exit anytime** by unwinding — taking the opposite side in the same market at the current price. Rates may have moved for or against you.
* **At maturity** the position [auto-rolls](fixed-maturity-and-auto-roll.md); there is no automatic settlement. Unwind to withdraw funds.

## Common questions

<details>

<summary>Why use ZC bonds instead of interest-bearing loans?</summary>

Two cash flows are cheaper and safer on-chain than many: less gas, no reinvestment risk for lenders, and clear upfront terms. The discount-to-par structure also makes yields directly comparable across maturities.

</details>

<details>

<summary>How is my yield affected if I sell before maturity?</summary>

Your realized yield depends on the price you sell at. If rates have fallen since you bought, the bond price has risen and you gain; if rates have risen, you may realize less than the original APR.

</details>

<details>

<summary>Where can I see the exact math used by the contracts?</summary>

The contracts compute durations in seconds (seconds-per-year = 31,536,000). See the [Developer Portal](../../developer-portal/introduction.md) for SDK and subgraph access to raw prices.

</details>

## Related

* [Order Book & Order Types](order-book.md) — how bonds actually trade
* [APR vs APY](../advanced-topics/apr-vs-apy.md) — why we quote APR
* [Tokenization](tokenization.md) — ZC bonds as ERC-20 tokens
