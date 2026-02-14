---
description: Client SDK for x402x Serverless Mode
---

# Client SDK

Client SDK for x402x Serverless Mode - Execute on-chain contracts directly via facilitator without needing a resource server.

---

## Installation

```bash
pnpm add @secured-finance/x402-client @secured-finance/x402-core
```

---

## Quick Start

### Basic Usage (React + wagmi)

```typescript
import { X402Client } from '@secured-finance/x402-client';
import { TransferHook, parseDefaultAssetAmount } from '@secured-finance/x402-core';
import { useWalletClient } from 'wagmi';
import { publicActions } from 'viem';

function PayButton() {
  const { data: wallet } = useWalletClient();

  const handlePay = async () => {
    // Extend wallet with public actions (required for transaction confirmation)
    const extendedWallet = wallet.extend(publicActions);

    // Uses default facilitator at https://facilitator.x402x.dev/
    const client = new X402Client({
      wallet: extendedWallet,
      network: 'base-sepolia'
    });

    // Convert USD amount to atomic units
    const atomicAmount = parseDefaultAssetAmount('1', 'base-sepolia'); // '1000000'

    const result = await client.execute({
      hook: TransferHook.getAddress('base-sepolia'),
      hookData: TransferHook.encode(),
      amount: atomicAmount, // Must be atomic units
      payTo: '0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb1'
    });

    console.log('Transaction:', result.txHash);
  };

  return <button onClick={handlePay}>Pay 1 USDC</button>;
}
```

Note: The wallet client must be extended with `publicActions` from viem to support transaction confirmation via `waitForTransactionReceipt`. If you're using the React hooks (`useX402Client`), this is done automatically.

---

## Amount Handling

The `amount` parameter must be in **atomic units** (smallest token unit). Use `parseDefaultAssetAmount()` to convert USD amounts:

```typescript
import { X402Client } from "@secured-finance/x402-client";
import { parseDefaultAssetAmount } from "@secured-finance/x402-core";

const client = new X402Client({ wallet, network: "base-sepolia" });

// Convert USD to atomic units
const amount = parseDefaultAssetAmount("1", "base-sepolia"); // '1000000' (1 USDC = 6 decimals)

// Correct usage
await client.execute({ 
  amount: amount,  // Pass atomic units
  payTo: "0x..." 
});
```

**Note**: Passing USD amounts directly (e.g., `amount: "1"`) will fail validation. Always convert first.

---

## API Reference

### High-Level API (Recommended)

#### X402Client

The main client class that handles the entire settlement flow.

```typescript
class X402Client {
  constructor(config: X402ClientConfig);
  execute(params: ExecuteParams): Promise<ExecuteResult>;
  calculateFee(hook: Address, hookData?: Hex): Promise<FeeCalculationResult>;
  waitForTransaction(txHash: Hex): Promise<TransactionReceipt>;
}
```

**Example:**

```typescript
import { X402Client } from "@secured-finance/x402-client";

// Uses default facilitator at https://facilitator.x402x.dev/
const client = new X402Client({
  wallet: walletClient,
  network: "base-sepolia",
});

// Or specify custom facilitator
const client = new X402Client({
  wallet: walletClient,
  network: "base-sepolia",
  facilitatorUrl: "https://custom-facilitator.example.com",
  timeout: 30000, // optional
  confirmationTimeout: 60000, // optional
});

// Convert USD amount to atomic units
import { parseDefaultAssetAmount } from "@secured-finance/x402-core";
const atomicAmount = parseDefaultAssetAmount("1", "base-sepolia"); // '1000000'

const result = await client.execute({
  hook: "0x...",
  hookData: "0x...",
  amount: atomicAmount, // Must be atomic units
  payTo: "0x...",
  facilitatorFee: "10000", // optional, will query if not provided (also atomic units)
  customSalt: "0x...", // optional, will generate if not provided
});
```

#### React Hooks

```typescript
import { useExecute } from '@secured-finance/x402-client';
import { parseDefaultAssetAmount } from '@secured-finance/x402-core';

function PayButton() {
  const { execute, status, error, result } = useExecute();

  const handlePay = async () => {
    const atomicAmount = parseDefaultAssetAmount('1', 'base-sepolia');
    await execute({ hook: '0x...', amount: atomicAmount, payTo: '0x...' });
  };

  return (
    <button onClick={handlePay} disabled={status !== 'idle'}>
      {status === 'idle' ? 'Pay' : 'Processing...'}
    </button>
  );
}
```

---

## Examples

### Simple Payment

```typescript
import { X402Client } from "@secured-finance/x402-client";
import { TransferHook, parseDefaultAssetAmount } from "@secured-finance/x402-core";

const client = new X402Client({ wallet: walletClient, network: "base-sepolia" });
const atomicAmount = parseDefaultAssetAmount("1", "base-sepolia");

const result = await client.execute({
  hook: TransferHook.getAddress("base-sepolia"),
  hookData: TransferHook.encode(),
  amount: atomicAmount,
  payTo: "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb1",
});
```

### Revenue Split

```typescript
const result = await client.execute({
  hook: TransferHook.getAddress("base-sepolia"),
  hookData: TransferHook.encode([
    { recipient: "0xPlatform...", bips: 3000 }, // 30%
  ]),
  amount: parseDefaultAssetAmount("100", "base-sepolia"),
  payTo: "0xCreator...", // Gets remaining 70%
});
```

---

## Related Packages

- [`@secured-finance/x402-core`](core.md) - Core utilities and commitment calculation
- [`@secured-finance/facilitator`](../../../x402-exec/facilitator) - Facilitator server implementation
- [x402](https://github.com/coinbase/x402) - Base x402 protocol

---

## Next Steps

- **[Quick Start Guide](../quick-start.md)** - Get started in 10 minutes
- **[Network Guide](../guides/network-guide.md)** - Network details
- **[Core Package](core.md)** - Advanced usage and utilities
