---
description: Two full numerical liquidation scenarios
---

# 📋 Liquidation Case Study

Both triggers of liquidation, worked end-to-end. Current threshold and fee values: [Protocol Parameters](../../protocol-parameters.md) (this page uses 80% threshold, 50% liquidation amount, 7% fee).

## Scenario 1 — Collateral value falls

**Setup:** Alice deposits 10 ETH at $2,000/ETH ($20,000) and borrows 12,000 USDC.

| Event        | Collateral | Debt    | LTV                    |
| ------------ | ---------- | ------- | ---------------------- |
| Entry        | $20,000    | $12,000 | 60%                    |
| ETH → $1,600 | $16,000    | $12,000 | 75%                    |
| ETH → $1,500 | $15,000    | $12,000 | **80% → liquidatable** |

**Liquidation:**

* Liquidator repays 6,000 USDC (50% of debt)
* Collateral seized: 6,000 × 1.07 / $1,500 = **4.28 ETH** ($6,420)
* Alice's remaining position: 5.72 ETH ($8,580) collateral, 6,000 USDC debt
* Post-liquidation LTV: 6,000 / 8,580 ≈ **70%**

## Scenario 2 — Borrowed asset rallies

Liquidation can also strike when the _debt_ appreciates, even if your collateral is a stablecoin.

**Setup:** Charlie deposits 1,000,000 USDC and borrows 10 BTC at $60,000/BTC ($600,000 debt).

| Event         | Collateral | Debt     | LTV                    |
| ------------- | ---------- | -------- | ---------------------- |
| Entry         | $1,000,000 | $600,000 | 60%                    |
| BTC → $75,000 | $1,000,000 | $750,000 | 75%                    |
| BTC → $80,000 | $1,000,000 | $800,000 | **80% → liquidatable** |

**Liquidation:**

* Liquidator repays 5 BTC ($400,000 — 50% of debt)
* Collateral seized: $400,000 × 1.07 = **$428,000 USDC**
* Charlie's remaining position: $572,000 USDC collateral, 5 BTC ($400,000) debt
* Post-liquidation LTV: 400,000 / 572,000 ≈ **70%**

## Takeaways

* **Watch both sides**: collateral falling _and_ debt rallying raise LTV. Borrowing a volatile asset against stablecoins is not a "safe" configuration.
* **Usually partial — not always**: at the 80% threshold, liquidation takes 50% of debt and the corresponding collateral + fee, and the position survives at a safer LTV. If LTV deteriorates past the **full-liquidation threshold** (≈ 85% — [Protocol Parameters](../../protocol-parameters.md)), the **entire debt** is liquidated in one call. Don't treat the 50% figure as your worst case.
* **The fee is avoidable**: adding collateral or unwinding early costs far less than the 7% liquidation fee.

## Related

* [Liquidation](./) — mechanism overview
* [ZC Bonds as Collateral](../zc-bonds-as-collateral.md) — liquidation specifics for ZC collateral
