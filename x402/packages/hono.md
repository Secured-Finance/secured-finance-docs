---
description: Hono middleware for x402x settlement framework
---

# Hono Middleware

Hono middleware for x402x settlement framework - easily add 402 payment gates to your Hono routes with dynamic facilitator fee calculation.

---

## Installation

```bash
npm install @secured-finance/x402-hono @secured-finance/x402-core
```

---

## Features

- Drop-in middleware for Hono routes
- Automatic settlement mode support
- Dynamic facilitator fee calculation - automatically queries current gas prices
- Works with builtin or custom hooks
- Edge runtime compatible
- Built-in caching for fee calculations

---

## Quick Start

```typescript
import { Hono } from "hono";
import { paymentMiddleware } from "@secured-finance/x402-hono";

const app = new Hono();

// Add payment gate with automatic fee calculation
app.use(
  "/api/premium",
  paymentMiddleware(
    "0xRecipient...", // Your recipient address
    {
      price: "$0.10", // Business price (facilitator fee auto-calculated)
      network: "base-sepolia",
    },
    { url: "https://facilitator.x402x.dev" }, // Facilitator for verify/settle/fee
  ),
);

app.post("/api/premium", (c) => {
  return c.json({ content: "Premium content!" });
});

export default app;
```

---

## Dynamic vs Static Fees

When using dynamic fee calculation (recommended), the facilitator fee is automatically calculated based on current gas prices. The total price shown to users is `price + facilitatorFee`.

For static fee mode, explicitly set `facilitatorFee`:

```typescript
{
  price: '$0.10',
  facilitatorFee: '$0.02',  // Fixed fee
}
```

---

## API Reference

### `paymentMiddleware(payTo, routes, facilitator?)`

Creates a Hono middleware that returns 402 responses with payment requirements.

#### Parameters

**`payTo`** (required): Final recipient address for payments

**`routes`** (required): Route configuration object:

- **`price`**: Business price (e.g., `'$0.10'`, `'0.1'`)
- **`network`**: Network name or array (e.g., `'base-sepolia'`, `['base-sepolia', 'polygon']`)
- **`facilitatorFee`** (optional):
  - Not set or `"auto"`: Dynamic calculation (recommended)
  - String/Money: Static fee (e.g., `'$0.01'`)
- **`hook`** (optional): Hook address (defaults to TransferHook)
- **`hookData`** (optional): Encoded hook data (defaults to `'0x'`)
- **`config`** (optional): Additional settings (description, timeout, etc.)

**`facilitator`** (optional but recommended): Facilitator configuration

- **`url`**: Facilitator service URL (e.g., `'https://facilitator.x402x.dev'`)
- **`createAuthHeaders`**: Optional auth header function

**Note**: Facilitator config is required for dynamic fee calculation and for verify/settle operations.

#### Returns

Hono middleware function compatible with Hono v4+

---

## Examples

```typescript
import { Hono } from "hono";
import { paymentMiddleware } from "@secured-finance/x402-hono";

const app = new Hono();

// Single route
app.use(
  "/api/data",
  paymentMiddleware(
    "0xYourAddress...",
    { price: "$0.10", network: "base-sepolia" },
    { url: "https://facilitator.x402x.dev" },
  ),
);

app.get("/api/data", (c) => {
  const x402 = c.get("x402");
  return c.json({ data: "Protected", payer: x402?.payer });
});

// Multiple routes with different prices
app.use(
  paymentMiddleware(
    "0xYourAddress...",
    {
      "/api/basic": { price: "$0.01", network: "base-sepolia" },
      "POST /api/premium": { price: "$0.10", network: "base-sepolia" },
    },
    { url: "https://facilitator.x402x.dev" },
  ),
);
```

---

## Related Packages

- [`@secured-finance/x402-core`](core.md) - Core utilities and types
- [`@secured-finance/x402-express`](express.md) - Express middleware
- [`@secured-finance/x402-fetch`](fetch.md) - Fetch wrapper for clients
- [`@secured-finance/x402-react`](react.md) - React hooks

---

## Next Steps

- **[Quick Start Guide](../quick-start.md)** - Get started in 10 minutes
- **[Network Guide](../guides/network-guide.md)** - Choose the right network
- **[Core Package](core.md)** - Advanced usage and utilities
