# ❓ FAQs

This page answers common questions about **SF Yield Vault**.

If you are new to Vaults, we recommend starting with the [**Getting Started**](getting-started/) section before reading this page.

***

## General

#### What is SF Yield Vault?

SF Yield Vault is an automated yield management product built around asset-specific Vault smart contracts. It allows users to deposit assets into Vaults and earn variable yield through underlying strategies.

When you deposit assets into a Vault, you receive **Vault shares** that represent your proportional ownership of the Vault. The value of these shares changes over time based on the performance of the underlying strategy.

***

#### How is SF Yield Vault different from Fixed-Rate Lending?

SF Yield Vault and Fixed-Rate Lending serve different purposes.

* **SF Yield Vault**
  * Variable yield
  * No fixed maturity
  * Automated strategy allocation
* **Fixed-Rate Lending**
  * Fixed interest rate
  * Defined maturity
  * Manual position management

Users can choose between the two depending on their risk and return preferences.

***

#### What assets can I deposit into a Vault?

Each Vault supports a single base asset.

Currently available:

* **JPYC Vault** — accepts JPYC deposits only
* **USDFC Vault** — accepts USDFC deposits only

***

## Deposits

#### What happens when I deposit into a Vault?

When you deposit into a Vault:

1. Your assets are transferred to the Vault contract
2. Vault shares are minted to your wallet
3. Deposited assets are allocated to the Vault’s strategy

You do not interact with the strategy directly.

***

#### What do I receive after depositing?

You receive **Vault shares**.

Vault shares represent your ownership of the Vault and can be redeemed for the underlying asset at any time.

***

#### Do I need to approve tokens before depositing?

Yes.

Before your first deposit, you must approve the Vault to use your assets.\
This is a standard requirement for ERC-20 tokens.

***

## Withdrawals

#### Can I withdraw my assets at any time?

Yes.

You can withdraw at any time by redeeming your Vault shares through the **Withdraw** tab.

***

#### Why is the amount I receive different from what I deposited?

Vaults generate **variable returns**.

* If the strategy performs well, you may receive more than your initial deposit
* If losses occur, you may receive less

Vaults do not guarantee principal or returns.

***

#### Can I partially withdraw my position?

Yes.

You can withdraw part of your Vault shares.\
The remaining shares will continue to accrue yield.

***

## Vault Shares and Yield

#### Why does my Vault share balance not change?

Yield is reflected in the **value of each share**, not in the number of shares.

Your share balance changes only when you deposit or withdraw.

***

#### How is yield distributed?

Yield is not paid out separately.

Instead, yield increases the total assets held by the Vault, which increases the value of Vault shares.

***

#### How is the Price Per Share (PPS) calculated?

The PPS represents the net asset value of a single Vault share and increases as the Vault generates yield:

$$
PPS = \frac{\text{Total Assets Held by the Vault}}{\text{Total Supply of Vault Shares}}
$$

***

#### How many shares will I receive upon deposit?

The number of shares minted to your wallet is determined by the PPS at the time of your deposit:

$$
\text{Shares Minted} = \frac{\text{Amount Deposited}}{PPS}
$$

***

#### How much will I receive upon withdrawal?

When you redeem your shares, the amount of the underlying asset you receive is calculated based on the latest PPS:

$$
\text{Amount Received} = \text{Shares Redeemed} \times PPS
$$

***

#### Does yield compound automatically?

Yes.

Because yield is reflected in share value, it compounds automatically without any user action.

***

## Strategy and Allocation

#### Can I choose or change the strategy?

No.

Strategy selection and allocation are managed by the Vault configuration.\
Users interact only with the Vault.

***

#### Why does the UI show “Unallocated” assets?

“Unallocated” assets are assets temporarily not deployed into a strategy.

This can occur during allocation updates or liquidity management and does not require user action.

***

## Risks

#### Is my deposit guaranteed?

No.

Vaults involve risks, including:

* Smart contract risk
* Strategy risk
* Liquidity risk
* Market risk

Users should understand these risks before depositing.

***

#### Can the value of my position decrease?

Yes.

If the underlying strategy incurs losses or market conditions change, the value of Vault shares may decrease.

***

## Fees

#### Are there any fees?

Fee information, if applicable, is displayed in the Vault interface under the **About** tab.

Fees are reflected in Vault performance and do not require separate user action.

***

## Technical

#### Do Vaults custody my assets?

Vaults are non-custodial smart contracts.

You always interact with Vaults directly through your wallet, and all transactions require your approval.
