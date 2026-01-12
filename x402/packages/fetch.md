---
description: Fetch wrapper for x402x settlement framework
---

# Fetch Wrapper

Fetch wrapper for x402x settlement framework - automatically handles 402 Payment Required responses with settlement mode support.

---

## Installation

```bash
npm install @secured-finance/x402-fetch @secured-finance/x402-core
```

---

## Features

- Automatic 402 response handling
- Commitment-based nonce for settlement mode
- Falls back to standard x402 for non-settlement payments
- Configurable maximum payment amount

---

## Quick Start

```typescript
import { wrapFetchWithPayment } from "@secured-finance/x402-fetch";
import { createWalletClient, custom } from "viem";

// Create wallet client (using wagmi, viem, etc.)
const walletClient = createWalletClient({
  account,
  transport: custom(window.ethereum),
});

// Wrap fetch with payment support
const fetchWithPay = wrapFetchWithPayment(fetch, walletClient);

// Make requests - 402 responses are handled automatically
const response = await fetchWithPay("/api/premium-content");
const data = await response.json();
```

---

## API Reference

### `wrapFetchWithPayment(fetch, walletClient, maxValue?, paymentRequirementsSelector?, config?)`

Wraps the native fetch API to automatically handle 402 Payment Required responses.

#### Parameters

- **`fetch`**: The fetch function to wrap (typically `globalThis.fetch`)
- **`walletClient`**: The wallet client used to sign payments (viem WalletClient or similar)
- **`maxValue`** (optional): Maximum allowed payment amount in base units (default: `0.1 USDC = 10^5`)
- **`paymentRequirementsSelector`** (optional): Function to select payment requirements from response
- **`config`** (optional): Optional configuration for X402 operations (e.g., custom RPC URLs)

#### Returns

A wrapped fetch function with the same signature as the native `fetch`.

#### Example

```typescript
// Basic usage
const fetchWithPay = wrapFetchWithPayment(fetch, walletClient);

// With custom max value (1 USDC)
const fetchWithPay = wrapFetchWithPayment(fetch, walletClient, BigInt(1 * 10 ** 6));

// With custom configuration
const fetchWithPay = wrapFetchWithPayment(fetch, walletClient, undefined, undefined, {
  svmConfig: { rpcUrl: "http://localhost:8899" }
});
```

### `x402xFetch(fetch, walletClient, maxValue?)`

Simplified alias for `wrapFetchWithPayment` (x402x style).

Note: This is a convenience function. For full compatibility with x402, use `wrapFetchWithPayment`.

```typescript
import { x402xFetch } from "@secured-finance/x402-fetch";

const fetchWithPay = x402xFetch(fetch, walletClient);
```

---

## Examples

```typescript
import { wrapFetchWithPayment } from '@secured-finance/x402-fetch';
import { useWalletClient } from 'wagmi';

function MyComponent() {
  const { data: walletClient } = useWalletClient();

  const fetchData = async () => {
    if (!walletClient) return;
    const fetchWithPay = wrapFetchWithPayment(fetch, walletClient);
    const response = await fetchWithPay('/api/protected-data');
    return response.json();
  };

  return <button onClick={fetchData}>Fetch Paid Content</button>;
}
```

## Settlement Mode vs Standard Mode

The wrapper automatically detects which mode to use:
- **Settlement Mode**: Uses commitment hash as nonce (when `extra.settlementRouter` exists)
- **Standard Mode**: Uses random nonce (standard x402 flow)

---

## Related Packages

- [`@secured-finance/x402-core`](core.md) - Core utilities and types
- [`@secured-finance/x402-react`](react.md) - React hooks for payments
- [`x402-fetch`](https://npmjs.com/package/x402-fetch) - Standard x402 fetch wrapper

---

## Next Steps

- **[Quick Start Guide](../quick-start.md)** - Get started in 10 minutes
- **[Client SDK](client.md)** - Higher-level client SDK
- **[React Hooks](react.md)** - React integration
- **[Core Package](core.md)** - Advanced usage and utilities
