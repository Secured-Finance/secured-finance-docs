---
description: How every position rolls at maturity with a single storage update
---

# Genesis Value & Compound Factor

These two constructs let the protocol roll *all* positions at maturity by updating **one number per market**, instead of touching every position — the accounting core of [Auto-Roll](../../core-concepts/fixed-maturity-and-auto-roll.md) and [Lazy Evaluation](lazy-evaluation.md).

## Compound Factor

At each quarterly roll, the protocol records the roll's effective discount rate as a multiplier and chains it onto a running product — the **Compound Factor**. Two are maintained per currency, differing by the roll fee:

**Lending Compound Factor (LCF):**

$$
LCF_{n+1} = LCF_{n} \times \left(\frac{1}{\text{AutoRollPrice}_{n}} - \text{AutoRollFeeRate}\right)
$$

**Borrowing Compound Factor (BCF):**

$$
BCF_{n+1} = BCF_{n} \times \left(\frac{1}{\text{AutoRollPrice}_{n}} + \text{AutoRollFeeRate}\right)
$$

The asymmetry (− fee for lenders, + fee for borrowers) is how the [auto-roll fee](../../core-concepts/fees.md) is charged without a separate transaction.

## Genesis Value

A position's **Genesis Value (GV)** expresses it in terms of the market's **Genesis Date** (the protocol's reference start date). When a position is created or rolls past maturity:

$$
GV = \frac{FV}{LCF_{\text{current}}}
$$

and at any later time its Future Value is recovered by:

$$
FV_{n} = GV \times LCF_{n}
$$

A lender's GV is positive and **never changes** — their FV grows purely through the LCF. A borrower's GV is negative and grows in magnitude with each roll, reflecting the fee spread between BCF and LCF:

$$
GV_{n+a} = GV_{n} + GV_{n}\left(\frac{BCF_{n+a}}{BCF_{n}} \cdot \frac{LCF_{n}}{LCF_{n+a}} - 1\right) \quad (GV_n < 0)
$$

## Worked example

1. Roll occurs at AutoRollPrice 98.00 with fee rate 0.001. A lender's LCF goes from 1.20 → 1.20 × (1/0.98 − 0.001) ≈ **1.2168**.
2. A lender with GV = 500: FV moves from 600 → 500 × 1.2168 = **608.4** — the position grew through the roll with *zero* per-position computation.
3. For 1,000 positions, a naive roll would cost ~20M gas (20k × 1,000 writes). Updating the Compound Factor once costs ~50k gas — a **99.7% reduction** — and individual FVs are derived on read.

## Design notes

* **One Genesis Date for everyone** standardizes the reference point; individual entry dates are captured by the LCF value at entry, not by per-user anchors.
* GV is protocol-computed, immutable per position, and fully auditable on-chain.
* ZC **perpetual tokens** ([Tokenization](../../core-concepts/tokenization.md)) are GV made transferable: an ERC-20 denominated in Genesis Value terms.

## Related

* [Auto-Roll Price Discovery](../../core-concepts/auto-roll-price-discovery.md) — where AutoRollPrice comes from
* [Lazy Evaluation](lazy-evaluation.md) — the read-time derivation this enables
