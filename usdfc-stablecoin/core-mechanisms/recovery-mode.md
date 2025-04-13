# 💞 Recovery Mode

**Recovery Mode** is activated when the **Total Collateral Ratio (TCR)** of the protocol falls below **150%**. It is designed to protect the protocol from a systemic risk of under-collateralization by prioritizing debt repayment and collateral distribution.

## Key Changes During Recovery Mode

1. **Liquidation Threshold Jump (110% to TCR)**\
   Troves with a collateral ratio below **TCR** are **immediately eligible for liquidation**, receiving a **10% penalty** upon liquidation.
2. **Zero Minting Fee**\
   The borrowing fee is set to **0%**, encouraging users to add collateral and stabilize the protocol.
3. **Minting Restrictions**\
   Borrowing that would lower the **TCR** is blocked. New USDFC can only be issued if it improves a Trove’s collateral ratio or establishes a new Trove at **150% or higher**.\
   Adjustments reducing collateral ratio are permitted only if the resulting TCR exceeds 150%.

## **Purpose**

The goal of Recovery Mode is to restore the **TCR to 150% or higher** and prevent a cascade of liquidations that could threaten the protocol’s stability.

**Risk to Trove Holders**

* Trove holders should maintain a **high collateral ratio** during Recovery Mode to avoid liquidation.
* **Low-collateral Troves** (below 150%) are more vulnerable and can be liquidated immediately.

**Example Scenario**

1. The TCR falls to **145%**, triggering Recovery Mode.
2. Troves below **TCR (145%)** are prioritized for liquidation.
3. Users are incentivized to add collateral to protect their positions and restore system stability.

## How do liquidations work in Recovery Mode? <a href="#how-do-liquidations-work-in-recovery-mode" id="how-do-liquidations-work-in-recovery-mode"></a>

* ICR = Individual Collateral Ratio
* MCR = Minimum Collateral Ratio (110%)
* TCR = Total Collateral Ratio
* SP = Stability Pool

<table><thead><tr><th width="277">Condition</th><th>Liquidation Behavior</th></tr></thead><tbody><tr><td>ICR &#x3C;=100%</td><td><strong>Redistribute</strong> all debt and collateral (minus gas compensation) to active Troves.</td></tr><tr><td>100% &#x3C; ICR &#x3C; MCR (110%)<br>&#x26; <br>SP USDFC > Trove debt </td><td>USDFC in the Stability Pool equal to the Trove's debt is offset with the Trove's debt. The Trove's FIL collateral (minus gas compensation) is shared between depositors.</td></tr><tr><td>100% &#x3C; ICR &#x3C; MCR (110%)<br>&#x26; <br>SP USDFC &#x3C; Trove debt</td><td>The total Stability Pool USDFC is offset with an equal amount of debt from the Trove. A fraction of the Trove's collateral (equal to the ratio of its offset debt to its entire debt) is shared between depositors. The remaining debt and collateral (minus gas compensation) is <strong>redistributed</strong> to active Troves.</td></tr><tr><td>MCR (110%) &#x3C;= ICR &#x3C; TCR <br>&#x26; <br>SP USDFC >= Trove debt</td><td>The Stability Pool USDFC is offset with an equal amount of debt from the Trove. A fraction of FIL collateral with dollar value equal to <code>1.1 * debt</code> is shared between depositors. Nothing is redistributed to other active Troves. Since its ICR was <code>> 1.1</code>, the Trove has a collateral remainder, which is sent to the <code>CollSurplusPool</code> and is claimable by the borrower. The Trove is closed.</td></tr><tr><td>MCR (110%) &#x3C;= ICR &#x3C; TCR <br>&#x26; <br>SP USDFC &#x3C; Trove debt</td><td>Do nothing.</td></tr><tr><td>ICR >= TCR</td><td>Do nothing.</td></tr></tbody></table>
