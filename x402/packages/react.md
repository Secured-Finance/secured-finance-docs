---
description: React hooks for x402x settlement framework
---

# React Hooks

React hooks for the x402x settlement framework.

---

## Features

- React hooks for payment flows
- Automatic mode detection
- Wagmi integration
- TypeScript support
- Lightweight with minimal dependencies

---

## Installation

```bash
npm install @secured-finance/x402-react @secured-finance/x402-core
# Also install peer dependencies if not already installed
npm install react wagmi viem
```

---

## Quick Start

```typescript
import { useX402Payment } from '@secured-finance/x402-react';
import { WagmiProvider } from 'wagmi';

function PaymentButton() {
  const { pay, status, error, result } = useX402Payment();

  const handlePay = async () => {
    try {
      const data = await pay('/api/protected-resource');
      console.log('Payment successful:', data);
    } catch (err) {
      console.error('Payment failed:', err);
    }
  };

  return (
    <div>
      <button
        onClick={handlePay}
        disabled={status === 'paying'}
      >
        {status === 'paying' ? 'Processing...' : 'Pay'}
      </button>

      {error && <p style={{ color: 'red' }}>{error}</p>}
      {result && <p>Success! {JSON.stringify(result)}</p>}
    </div>
  );
}

function App() {
  return (
    <WagmiProvider config={wagmiConfig}>
      <PaymentButton />
    </WagmiProvider>
  );
}
```

---

## API Reference

### `useX402Payment(options?)`

Main hook for handling x402x payments.

#### Parameters

- `options.maxValue` (optional): Maximum allowed payment amount in base units (default: 0.1 USDC)

#### Returns

```typescript
{
  status: 'idle' | 'paying' | 'success' | 'error',
  error: string | null,
  result: any,
  pay: (url: string, init?: RequestInit) => Promise<any>,
  reset: () => void,
  isConnected: boolean,
  address: string | undefined,
}
```

#### Properties

- `status`: `'idle' | 'paying' | 'success' | 'error'`
- `error`: Error message if payment failed
- `result`: Payment result data if successful
- `pay(url, init?)`: Function to make a payment
- `reset()`: Reset payment state to idle
- `isConnected`: Whether wallet is connected
- `address`: User's wallet address

---

## Examples

```typescript
function PaymentButton() {
  const { pay, status, error } = useX402Payment();

  return (
    <div>
      <button onClick={() => pay('/api/content')} disabled={status === 'paying'}>
        {status === 'paying' ? 'Processing...' : 'Pay'}
      </button>
      {error && <div className="error">{error}</div>}
    </div>
  );
}
```

---

## Requirements

- React 18+
- Wagmi 2+
- A configured Wagmi provider wrapping your app

---

## Related Packages

- [`@secured-finance/x402-core`](core.md) - Core utilities and types
- [`@secured-finance/x402-client`](client.md) - Client SDK (used internally)
- [`@secured-finance/x402-fetch`](fetch.md) - Fetch wrapper (used internally)
- [x402](https://github.com/coinbase/x402) - Base x402 protocol

---

## Next Steps

- **[Quick Start Guide](../quick-start.md)** - Get started in 10 minutes
- **[Client SDK](client.md)** - Lower-level client API
- **[Core Package](core.md)** - Advanced usage and utilities
