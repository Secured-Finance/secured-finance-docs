---
description: Understanding how Zero-Coupon Bonds can be tokenized as ERC20 tokens in the Fixed-Rate Lending Protocol
icon: 🪙
---

# 🪙 ZC Bond Tokenization

## Overview

Our protocol allows Zero Coupon Bonds (Lending positions) to be tokenized as ERC20 standard tokens, which is called `ZCToken`, and withdrawn from the platform. This tokenization enables greater flexibility for users, allowing them to transfer their lending positions to other wallets or potentially trade them on secondary markets.



## How It Works

The tokenization process involves converting lending positions into standard ERC20 tokens that can be withdrawn from the platform and later redeposited if desired. There are two main flows in this process:

### Token Withdrawal Flow

When a user wants to withdraw their lending position as a token:

<figure><img src="../../.gitbook/assets/ZCToken mint.png" alt=""><figcaption><p>ZC Token Minting Process</p></figcaption></figure>

### Token Deposit Flow

When a user wants to deposit their ZC token back into the platform:

<figure><img src="../../.gitbook/assets/ZCToken burn.png" alt=""><figcaption><p>ZC Token Burning Process</p></figcaption></figure>

### Token Types

Each ZC token has a maturity, but if the maturity is 0, it becomes a ZC perpetual token. Generally ZC tokens are minted from `FutureValueVault` but ZC perpetual tokens are minted from `GenesisValueVault`. Please check the [Genesis Value page](../advanced-topics/orderbook-deep-dive/genesis-value.md) for the reference.

### Token Naming Conventions

**ZC Token Names and Symbols (example as March 2024 expiry):**

<table data-full-width="false"><thead><tr><th width="96">Asset</th><th width="184">ZC Token Name</th><th width="167" align="center">ZC Token Symbol</th><th width="157" align="center">ZC Perpetual Token Name</th><th>ZC Perpetual Token Symbol</th></tr></thead><tbody><tr><td>ETH</td><td>ZC ETH MAR2024</td><td align="center">zcETH-2024-03</td><td align="center">ZC ETH</td><td>zcETH</td></tr><tr><td>WBTC</td><td>ZC WBTC MAR2024</td><td align="center">zcWBTC-2024-03</td><td align="center">ZC WBTC</td><td>zcWBTC</td></tr><tr><td>USDC</td><td>ZC USDC MAR2024</td><td align="center">zcUSDC-2024-03</td><td align="center">ZC USDC</td><td>zcUSDC</td></tr><tr><td>axlFIL</td><td>ZC axlFIL MAR2024</td><td align="center">zcaxlFIL-2024-03</td><td align="center">ZC axlFIL</td><td>zcaxlFIL</td></tr></tbody></table>

**Metamask Symbol Name Convention (max 11 chars, example as March 2024 expiry):**

| Asset  | ZC Token Name     | Metamask Symbol |
| ------ | ----------------- | --------------- |
| ETH    | ZC ETH MAR2024    | zcETH24M        |
| WBTC   | ZC WBTC MAR2024   | zcWBTC24M       |
| USDC   | ZC USDC MAR2024   | zcUSDC24M       |
| axlFIL | ZC axlFIL MAR2024 | zcxFIL24M       |
| FIL    | ZC FIL MAR2024    | zcFIL24M        |

Month abbreviations: MAR = M; JUN = J; SEP = S; DEC = D

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Token Standard | The token standard used for ZC tokens | ERC20 |
| Token Decimals | Number of decimal places supported by ZC tokens | 18 |
| Maturity Format | How maturity is represented in token names | MMMYYYY (e.g., MAR2024) |
| Symbol Format | Format for token symbols | zc[ASSET]-YYYY-MM |
| Metamask Symbol Format | Shortened format for Metamask display | zc[ASSET]YYM |
| Perpetual Token Maturity | Maturity value for perpetual tokens | 0 |
| Minting Source (ZC Tokens) | Contract that mints standard ZC tokens | FutureValueVault |
| Minting Source (Perpetual) | Contract that mints perpetual ZC tokens | GenesisValueVault |

## Examples

### Example 1: Withdrawing a Lending Position as a ZC Token

Alice has lent 1,000 USDC in the JUN2025 market and wants to transfer this position to another wallet:

1. Alice navigates to the "My Positions" section in the protocol interface
2. She selects her 1,000 USDC lending position in the JUN2025 market
3. She clicks "Withdraw as Token" and confirms the transaction
4. The protocol mints a "ZC USDC JUN2025" token (zcUSDC-2025-06) to Alice's wallet
5. The token represents Alice's right to receive 1,000 USDC plus interest at maturity
6. Alice can now transfer this token to any other Ethereum wallet

### Example 2: Depositing a ZC Token Back into the Protocol

Bob has received a "ZC ETH SEP2024" token from a friend and wants to manage it within the protocol:

1. Bob navigates to the "Deposit" section in the protocol interface
2. He selects the "Deposit ZC Token" option
3. He selects his "ZC ETH SEP2024" token from his wallet
4. He confirms the transaction
5. The protocol burns the ZC token and credits Bob's account with the corresponding lending position
6. Bob can now view and manage this position within the protocol interface

### Example 3: Using ZC Perpetual Tokens

Charlie wants to create a more flexible lending position that isn't tied to a specific maturity:

1. Charlie deposits 5 ETH into the GenesisValueVault
2. The protocol mints "ZC ETH" perpetual tokens (zcETH) to Charlie's wallet
3. These tokens represent a standardized lending position without a fixed maturity date
4. Charlie can transfer these tokens to other users or use them in other DeFi protocols
5. When Charlie wants to redeem the underlying value, he can deposit the tokens back into the GenesisValueVault

## FAQ

### What is the difference between ZC tokens and ZC perpetual tokens?

ZC tokens have a specific maturity date (e.g., ZC ETH MAR2024) and represent a lending position that will mature on that date. ZC perpetual tokens (e.g., ZC ETH) do not have a specific maturity date and represent a standardized lending position that can be redeemed at any time. ZC tokens are minted from the FutureValueVault, while ZC perpetual tokens are minted from the GenesisValueVault.

### Can I trade ZC tokens on secondary markets?

Yes, ZC tokens are standard ERC20 tokens that can be transferred to any Ethereum wallet and potentially traded on secondary markets or used in other DeFi protocols. However, the liquidity of these tokens on secondary markets may vary depending on market conditions and the specific token.

### What happens to my ZC token at maturity?

When a ZC token reaches its maturity date, it can be redeemed for the underlying asset plus any accrued interest. The protocol will handle the redemption process when you deposit the token back into the platform. Alternatively, if you participate in Auto-Rolling, your position can be automatically rolled over to a new maturity.

### How do I add ZC tokens to my Metamask wallet?

ZC tokens should appear automatically in your Metamask wallet after they are minted. However, if they don't appear, you can add them manually:
1. Click "Import tokens" in Metamask
2. Enter the token contract address (available from the protocol interface)
3. The token symbol and decimals should auto-populate
4. Click "Add Custom Token"

Note that Metamask has a character limit for token symbols, so the symbols may appear slightly different (e.g., "zcETH24M" instead of "zcETH-2024-03").

### Can I partially withdraw my lending position as a ZC token?

Yes, you can withdraw any portion of your lending position as a ZC token. The protocol will mint tokens representing the exact amount you choose to withdraw, and the remaining portion will stay in your account within the protocol.

## Related Resources

- [Standardization](standardization/README.md)
- [Zero-Coupon Bonds](standardization/zero-coupon-bonds.md)
- [Order Book System](order-book-system/README.md)
- [Genesis Value](../advanced-topics/orderbook-deep-dive/genesis-value.md)
- [Auto-Rolling](../advanced-topics/market-dynamics/auto-rolling/README.md)
