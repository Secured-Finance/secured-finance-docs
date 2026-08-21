---
description: Frequently asked questions about SF Yield Vault
---

# ❓ FAQs

Common questions about **SF Yield Vault**. New to vaults? Start with [Getting Started](getting-started/README.md).

## General

<details>

<summary>What is SF Yield Vault?</summary>

An automated yield product built on asset-specific, ERC-4626 vault contracts. You deposit an asset, receive **vault shares** representing proportional ownership, and earn variable yield as the vault's strategies deploy the assets. The value of your shares changes with strategy performance. See the [Overview](overview.md).

</details>

<details>

<summary>How is SF Yield Vault different from Fixed-Rate Lending?</summary>

The vault gives you **variable** yield with no maturity and fully automated management; Fixed-Rate Lending gives you a **fixed** rate for a defined term with direct position management. The current vault strategies actually lend into the Fixed-Rate Lending markets on your behalf — the vault is the hands-off way in. Comparison table in the [Overview](overview.md#sf-yield-vault-or-fixed-rate-lending).

</details>

<details>

<summary>What assets can I deposit?</summary>

Each vault takes a single base asset: the **JPYC Vault** accepts JPYC (Ethereum), the **USDFC Vault** accepts USDFC (Filecoin). See [Available Vaults and Strategies](core-mechanics/available-vaults-and-strategies/README.md).

</details>

## Deposits

<details>

<summary>What happens when I deposit?</summary>

Your assets transfer to the vault contract and vault shares are minted to your wallet. The vault may then allocate the assets to its strategy — funds can also sit unallocated for a time during allocation updates or liquidity management. You never interact with the strategy directly. Walkthrough: [Deposit assets](getting-started/deposit-assets.md).

</details>

<details>

<summary>Do I need to approve tokens before depositing?</summary>

Yes — a one-time approval per asset per vault, before your first deposit. The app prompts you with **Approve** when it's needed.

</details>

## Withdrawals

<details>

<summary>Can I withdraw at any time?</summary>

Yes in the sense that there is no lock-up or fixed term — you can request a withdrawal whenever you like. Completion depends on strategy liquidity: if the underlying order book cannot absorb the unwind, the transaction reverts and you can retry later or in a smaller size. See [Withdraw assets](getting-started/withdrawing-assets.md).

</details>

<details>

<summary>Why is the amount I receive different from what I deposited?</summary>

You receive shares × current value per share. If yield accrued, you get more than you put in; if the strategy took losses, less. Small differences from the on-screen estimate are timing effects between quote and execution.

</details>

<details>

<summary>Can I withdraw only part of my position?</summary>

Yes. Redeem any portion of your shares; the rest keeps accruing yield.

</details>

## Shares and yield

<details>

<summary>Why doesn't my share balance change?</summary>

By design. Yield appears in the **value of each share**, not the share count — your balance moves only when you deposit or withdraw. Because gains fold into the share price, yield also **compounds automatically**.

</details>

<details>

<summary>How is the price per share (PPS) calculated?</summary>

$$
PPS = \frac{\text{Total Assets (idle + reported strategy balances)}}{\text{Total Supply of Vault Shares}}
$$

Deposits mint $$\text{Amount} / PPS$$ shares; withdrawals return $$\text{Shares} \times PPS$$ assets, always at the PPS current at execution.

</details>

## Strategy and allocation

<details>

<summary>Can I choose or change the strategy?</summary>

No. Strategy selection and allocation are part of the vault's configuration — you interact only with the vault. What each strategy does is documented in [Available Vaults and Strategies](core-mechanics/available-vaults-and-strategies/README.md).

</details>

<details>

<summary>Why does the app show "Unallocated" assets?</summary>

Assets temporarily not deployed to a strategy — normal during allocation updates or liquidity management, and no action is needed from you.

</details>

## Fees

<details>

<summary>Are there any fees?</summary>

No deposit, withdrawal, or management fees. The strategies charge a **5% performance fee on realized profits**, deducted before gains reach the vault — the value per share is always net of fees. Details in [Fees](core-mechanics/vault-system-overview.md#fees); current values also appear in the app's **About** tab.

</details>

## Risks

<details>

<summary>Is my deposit guaranteed?</summary>

No. Vault positions carry smart contract, strategy, liquidity, and market risk — the value of your position can decrease if the strategy takes losses or conditions turn. Withdrawals are not guaranteed at all times either: they depend on order-book liquidity. Each strategy's page lists its specific risks — [JPYC](core-mechanics/available-vaults-and-strategies/jpyc-lending-strategy.md#risk-considerations), [USDFC](core-mechanics/available-vaults-and-strategies/usdfc-lending-strategy.md#risk-considerations) — and the protocol-wide [Risk Disclaimer](../resources/legal/risk-disclaimer.md) applies.

</details>

## Technical

<details>

<summary>Do vaults custody my assets?</summary>

Vaults are **non-custodial** smart contracts. You interact with them directly from your wallet, and every transaction requires your signature. Addresses are listed in [Contracts and Security](contracts-and-security.md).

</details>
