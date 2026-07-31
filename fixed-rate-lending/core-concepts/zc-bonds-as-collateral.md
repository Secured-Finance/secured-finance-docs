---
description: Use your lending positions as collateral for yield-spread strategies
---

# ZC Bonds as Collateral

Your Zero-Coupon bond holdings (lending positions) can serve as **collateral for borrowing** — you don't need to sell a position to unlock liquidity from it. This is the foundation of yield-spread strategies: lend at one maturity, borrow against the position at another, and capture the spread.

## Valuation rules

| Situation | Haircut |
| --- | --- |
| Borrowing in the **same currency** as the ZC bond | **20%** — the bond counts for up to 80% of its present value |
| Borrowing in a **different currency** | **100%** — cross-currency ZC collateral is not currently accepted |

ZC bonds are consumed as collateral **first**, before your cash collateral, up to 80% of their PV. The system tracks this as the **ZC utilization ratio**:

$$
\text{ZC Utilization} = \frac{\text{Obligation}}{\text{Total ZC}}
$$

When ZC collateral is in play, LTV incorporates it alongside cash:

$$
\text{LTV} = \frac{\text{Obligation}}{\text{Cash Collateral} + \text{Consumed ZC Collateral}}
$$

{% hint style="info" %}
You can borrow in the same currency **without any cash collateral at all** — a ZC bond alone supports borrowing up to 80% of its PV.
{% endhint %}

## Worked example

User A holds a ZC bond with a present value of 1,000 USDC and no cash collateral:

1. Maximum borrow: 800 USDC (80% of PV). They borrow the full 800 USDC.
2. ZC utilization: 800 / 1,000 = **80%**.
3. The borrowed 800 USDC itself sits in the protocol vault, so overall collateral utilization is 800 / (1,000 + 800) ≈ **44%** — a more comfortable overall position than the ZC utilization alone suggests.

**Liquidation scenario:** if the ZC bond's price falls and utilization exceeds the threshold, 50% of the obligation (400 USDC) can be liquidated — or **100%** if utilization deteriorates past the full-liquidation threshold — with the standard liquidation fee taken from the ZC collateral. The same rules apply as for any other collateral ([Liquidation](liquidation/README.md), current values in [Protocol Parameters](../protocol-parameters.md)).

## Risks to understand

* **Rate risk** — ZC bond prices move inversely to yields; a rate spike lowers your collateral value.
* **Cross-currency liquidation** — liquidators may choose which obligation and which collateral currency to act on. A breach triggered in one currency can result in liquidation involving another.
* **Maturity drift** — as bonds approach maturity their price rises toward par, which generally *helps* collateral value, but rolls restate positions at market rates.

## Related

* [Collateral](collateral.md) — the general collateral framework
* [Liquidation](liquidation/README.md) — thresholds and process
* [Fixed Maturity & Auto-Roll](fixed-maturity-and-auto-roll.md) — what happens to collateralized positions at maturity
