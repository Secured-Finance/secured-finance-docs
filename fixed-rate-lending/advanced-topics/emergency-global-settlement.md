---
description: The last-resort shutdown that returns user funds
---

# Emergency Global Settlement

Emergency Global Settlement is the protocol's last-resort safeguard for catastrophic events — a critical exploit, an unrecoverable bug, or a systemic oracle failure. When executed by the protocol admin, **all markets halt permanently** and the protocol enters a redemption-only state.

## The process

1. **Halt** — all markets and the Token Vault stop. Price feeds are snapshotted for reference.
2. **Redemption** — each user's total assets and positions are valued (in present value, using the snapshotted prices) and replaced with a **proportional basket of the collateral tokens held in the Token Vault**. This applies to everyone, including users with deposits but no positions.
3. **Withdrawal** — users withdraw their replaced tokens. There is no deadline on redemption.

### Example

Token Vault holds $100,000 USDC and $200,000 of ETH (1:2 ratio). A user's total funds are $15,000 (a $10,000 lending position + $5,000 of deposits). After settlement, the user's claims are replaced with **$5,000 in USDC and $10,000 in ETH**, which they can withdraw at any time.

## Important properties

* **Irreversible** — once triggered, markets never reopen; resuming operations would require new contract deployments. This one-way design lets users withdraw with certainty that the state won't change again.
* **Proportional** — everyone receives the same collateral-token ratios; no queue-jumping.
* **Loss scenarios** — if the vault itself lost funds (e.g. via the exploit that triggered settlement), redemptions are proportionally reduced. Settlement guarantees fair distribution of what remains, not immunity from the loss itself.

## Related

* [Contracts & Security](../contracts-and-security.md) — audits and bug bounty
* [Circuit Breaker](circuit-breaker.md) and [Base Price Adjustment](base-price-adjustment.md) — the everyday safety layers that make this one a last resort
