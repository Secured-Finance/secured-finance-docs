---
description: Two full numerical liquidation scenarios
---

# Liquidation Case Study

Both triggers of liquidation, worked end-to-end. Current threshold and fee values: [Protocol Parameters](../../protocol-parameters.md) (this page uses 80% threshold, 50% liquidation amount, 7% fee).

## Scenario 1 — Collateral value falls

**Setup:** Alice deposits 10 ETH at $2,000/ETH ($20,000) and borrows 12,000 USDC.

| Event | Collateral | Debt | LTV |
| --- | --- | --- | --- |
| Entry | $20,000 | $12,000 | 60% |
| ETH → $1,600 | $16,000 | $12,000 | 75% |
| ETH → $1,500 | $15,000 | $12,000 | **80% → liquidatable** |

**Liquidation:**

* Liquidator repays 6,000 USDC (50% of debt)
* Collateral seized: 6,000 × 1.07 / $1,500 = **4.28 ETH** ($6,420)
* Alice's remaining position: 5.72 ETH ($8,580) collateral, 6,000 USDC debt
* Post-liquidation LTV: 6,000 / 8,580 ≈ **70%**

## Scenario 2 — Borrowed asset rallies

Liquidation can also strike when the *debt* appreciates, even if your collateral is a stablecoin.

**Setup:** Charlie deposits 1,000,000 USDC and borrows 10 BTC at $60,000/BTC ($600,000 debt).

| Event | Collateral | Debt | LTV |
| --- | --- | --- | --- |
| Entry | $1,000,000 | $600,000 | 60% |
| BTC → $75,000 | $1,000,000 | $750,000 | 75% |
| BTC → $80,000 | $1,000,000 | $800,000 | **80% → liquidatable** |

**Liquidation:**

* Liquidator repays 5 BTC ($400,000 — 50% of debt)
* Collateral seized: $400,000 × 1.07 = **$428,000 USDC**
* Charlie's remaining position: $572,000 USDC collateral, 5 BTC ($400,000) debt
* Post-liquidation LTV: 400,000 / 572,000 ≈ **70%**

## Takeaways

* **Watch both sides**: collateral falling *and* debt rallying raise LTV. Borrowing a volatile asset against stablecoins is not a "safe" configuration.
* **Partial, not total**: liquidation takes up to 50% of debt and the corresponding collateral + fee — the position survives, at a safer LTV.
* **The fee is avoidable**: adding collateral or unwinding early costs far less than the 7% liquidation fee.

## Related

* [Liquidation](README.md) — mechanism overview
* [ZC Bonds as Collateral](../zc-bonds-as-collateral.md) — liquidation specifics for ZC collateral
