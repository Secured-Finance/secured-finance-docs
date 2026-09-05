---
description: Frequently asked questions about the USDFC stablecoin
---

# ❓ FAQs

## Getting Started

<details>

<summary>What is USDFC?</summary>

USDFC is a decentralized stablecoin pegged to the US Dollar and backed entirely by Filecoin (FIL) collateral, running on the Filecoin Virtual Machine.

**Key properties:**

* **Over-collateralized** — every USDFC is backed by at least 110% of its value in FIL
* **Redeemable** — exchangeable for $1 of FIL directly from the protocol (whenever the system's total collateral ratio is above 110%)
* **Interest-free** — a one-time borrowing fee, no ongoing charges
* **No central issuer** — minting, liquidation, and redemption are all on-chain mechanisms

**Related:** [Overview](overview.md)

</details>

<details>

<summary>What is Secured Finance?</summary>

Secured Finance is the DeFi platform behind USDFC. It runs three products: the **USDFC Stablecoin** on Filecoin, **Fixed-Rate Lending** (fixed-rate, fixed-term markets on Ethereum, Arbitrum, and Filecoin), and the **SF Yield Vault** (automated variable-yield vaults).

**Related:** [Protocol at a Glance](../introduction/protocol-at-a-glance.md)

</details>

<details>

<summary>How does USDFC maintain its peg to the US Dollar?</summary>

Through interlocking mechanisms rather than a single lever:

1. **Over-collateralization** — at least 110% FIL backing at all times
2. **Redemption** — anyone can exchange USDFC for $1 of FIL, so trading below $1 creates instant arbitrage that burns supply and lifts the price
3. **Minting arbitrage** — trading above $1 makes minting-and-selling profitable, expanding supply and lowering the price
4. **Liquidation and the Stability Pool** — remove under-collateralized debt before it can undermine the backing

**Related:** [System Overview](core-mechanics/system-overview.md), [Redemption](core-mechanics/redemption.md)

</details>

<details>

<summary>How do I get started?</summary>

You need a web3 wallet (e.g. MetaMask) holding FIL. Connect it to the [USDFC app](https://app.usdfc.net), open a Trove by depositing FIL, and mint USDFC against it. The full walkthrough is in [Creating Your First Trove](getting-started/creating-your-first-trove.md) — or practice first with free tokens on [testnet](getting-started/getting-test-usdfc-on-testnet.md).

</details>

## Minting & Borrowing

<details>

<summary>How do I mint USDFC, and what does it cost?</summary>

Open a Trove with FIL collateral and choose how much to borrow (minimum 200 USDFC, ratio above 110%). Costs:

* **Borrowing fee** — (Base Rate + 0.5%) of the minted amount, typically 0.5%, capped at 5%. Added to your debt.
* **Liquidation Reserve** — 20 USDFC added to your debt and refunded when you close the Trove.
* **Gas** — network fees in FIL.

There is **no interest** — the borrowing fee is the entire cost, however long you keep the loan.

**Worked example:** deposit 100 FIL worth $500 and mint 200 USDFC. Fee = 1 USDFC, so total debt = 200 + 20 + 1 = 221 USDFC and your collateral ratio is 500 / 221 ≈ 226%. The full 200 USDFC arrives in your wallet — fees are added to debt, never deducted from what you receive.

**Related:** [Mint & Borrow](core-mechanics/mint-and-borrow.md)

</details>

<details>

<summary>Can I mint more from an existing Trove?</summary>

Yes — increase the borrowed amount via **Update Trove** any time your resulting ratio stays above the minimum. The borrowing fee applies to the newly minted amount only.

**Related:** [Minting USDFC Step-by-Step](getting-started/minting-usdfc-step-by-step.md)

</details>

<details>

<summary>How do I close my Trove?</summary>

Repay the full debt in one transaction (partial closure isn't a thing — but partial *repayment* via Update Trove is). The 20 USDFC Liquidation Reserve is netted out at closing, and all your collateral returns to your wallet. Note you must cover the borrowing fees, which is slightly more USDFC than you originally received — see [the Trove lifecycle](core-mechanics/the-trove-system.md#debt-calculations).

</details>

## Risk Management

<details>

<summary>What is the minimum collateral ratio, and what should I actually maintain?</summary>

The hard minimum is **110%** — below it your Trove can be liquidated. During [Recovery Mode](core-mechanics/recovery-mode.md), Troves below the system's total collateral ratio (up to 150%) can be liquidated too, and new Troves must open at 150%+.

The app labels **200%+** as very low risk, **150–200%** low, **120–150%** medium, and below 120% high. Where you sit is a trade-off between capital efficiency and how closely you can monitor the market.

**Related:** [Managing Collateral Effectively](getting-started/managing-collateral-effectively.md)

</details>

<details>

<summary>How do liquidations work?</summary>

When a Trove falls below 110%, anyone can trigger its liquidation: its debt is repaid by burning USDFC from the [Stability Pool](core-mechanics/stability-pool.md), its FIL goes to the pool's depositors, and the trigger-er collects the 20 USDFC reserve plus 0.5% of the collateral.

**Worked example:** a Trove holds 100 FIL worth $400 against 380 USDFC of debt — ratio 105%. On liquidation, the pool burns 380 USDFC and receives roughly $398 of FIL (after the liquidator's 0.5%). The borrower keeps the 380 USDFC they borrowed but loses the $400 of collateral.

**Related:** [Liquidation](core-mechanics/liquidation.md)

</details>

<details>

<summary>What do Stability Pool depositors earn — and risk?</summary>

When liquidations occur, depositors' USDFC is burned to repay the debt and they receive the liquidated FIL in exchange — normally worth **up to ~10% more** than the USDFC consumed, since liquidation happens just below 110%. The exact premium depends on the ratio at liquidation; in a severe crash a Trove can be liquidated below 100%, making that liquidation a net loss.

The risks: your stable deposit gradually converts into **volatile FIL** at times you don't choose, FIL can fall after you receive it, and withdrawals are briefly suspended while liquidatable Troves are pending. Rewards only accrue when liquidations actually happen.

**Related:** [Stability Pool](core-mechanics/stability-pool.md), [Using the Stability Pool](getting-started/using-the-stability-pool.md)

</details>

<details>

<summary>What happens if the Stability Pool is empty during a liquidation?</summary>

The protocol falls back to **redistribution**: the liquidated Trove's debt and collateral are spread across all active Troves, in proportion to each Trove's **collateral**. Receiving Troves gain both debt and collateral — the USD value received exceeds the debt taken on, but their collateral *ratio* drops. Everything is automatic; no action is required from Trove owners.

**Related:** [Stability Pool](core-mechanics/stability-pool.md#if-the-pool-runs-dry-redistribution)

</details>

<details>

<summary>What if FIL crashes hard?</summary>

Liquidations fire on the Troves that fall below threshold, the Stability Pool absorbs them, and if the system-wide ratio drops below 150%, [Recovery Mode](core-mechanics/recovery-mode.md) activates — extending liquidation up to the TCR, blocking collateral withdrawal, and waiving fees on repairs. These are the designed responses, not guarantees: in an extreme enough crash, Stability Pool depositors can take losses and remaining Troves absorb redistributed debt. Position sizing and buffer are your real protection.

</details>

## Advanced Topics

<details>

<summary>What is redemption and how does it work?</summary>

Any holder can exchange USDFC for $1 worth of FIL directly from the protocol. The FIL comes from the **lowest-collateral-ratio Troves** (at or above 110%; below that they're left for liquidation), whose debt is reduced by the same value — a forced swap for those owners, not a loss. The fee is (Base Rate + 0.5%), minimum 0.5%, deducted from the FIL.

If you own a Trove, keeping your ratio above the crowd's — and watching the app's **Debt in front** figure — keeps you out of the redemption queue.

**Related:** [Redemption](core-mechanics/redemption.md)

</details>

<details>

<summary>What is Recovery Mode?</summary>

A system-wide state that activates when total collateralization falls below 150%: the liquidation threshold extends up to the TCR, new Troves need 150%+, collateral withdrawal is blocked, and the borrowing fee drops to 0% so repairing positions is frictionless. It ends automatically once the TCR recovers above 150%. The app shows a banner while it's active.

**Related:** [Recovery Mode](core-mechanics/recovery-mode.md)

</details>

<details>

<summary>Can I use USDFC for gasless transfers or x402 payments?</summary>

Yes. USDFC implements **EIP-3009** (`transferWithAuthorization` / `receiveWithAuthorization`) and **EIP-2612** (`permit`), so a holder can authorize a transfer with an off-chain signature and let any party submit it and pay the gas — the building blocks of gasless flows and **x402** (HTTP 402) payments. For integration details, see the [USDFC SDK](../developer-portal/sdk-reference/usdfc-sdk.md).

**Related:** [Contracts and Security](deployed-contracts.md#token-standards)

</details>

<details>

<summary>Where does the FIL/USD price come from?</summary>

From the protocol's PriceFeed contract, which uses Secured Finance's own price oracle as the primary source with Tellor as fallback — including defined behavior when prices go stale. See [Price Oracle](core-mechanics/price-oracle.md) for the mechanics and trust assumptions.

</details>
