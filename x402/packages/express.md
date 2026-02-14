---
description: Express middleware for x402x settlement framework
---

# Express Middleware

Express middleware for the x402x settlement framework. Provides full x402 payment protocol support with x402x settlement extensions.

---

## Features

- Full x402 payment flow with automatic verification and settlement
- X402Context extension for accessing payment details in route handlers
- Multi-network support
- Custom settlement hooks
- Dollar-denominated pricing
- Dynamic fee calculation with caching
- TypeScript support

---

## Installation

```bash
pnpm add @secured-finance/x402-express
```

---

## Quick Start

```typescript
import express from "express";
import { paymentMiddleware } from "@secured-finance/x402-express";

const app = express();

// Single route with automatic fee calculation (recommended)
app.post(
  "/api/premium",
  paymentMiddleware(
    "0xYourRecipientAddress", // Final payment recipient
    {
      price: "$0.10", // Your business price (0.10 USD)
      network: "base-sepolia", // Payment network
      // facilitatorFee auto-calculated based on gas prices
      config: {
        description: "Access to premium content",
      },
    },
    {
      url: "https://facilitator.x402x.dev", // Facilitator for verify/settle/fee
    },
  ),
  (req, res) => {
    // Access verified payment context (x402x extension)
    const { payer, amount, network } = req.x402!;

    console.log(`Received payment from ${payer}: ${amount} on ${network}`);

    res.json({
      success: true,
      message: "Payment received and settled",
    });
  },
);

app.listen(3000);
```

---

## Dynamic vs Static Fees

When using dynamic fee calculation (recommended), the facilitator fee is automatically calculated based on current gas prices. The total price shown to users is `price + facilitatorFee`.

For static fee mode, explicitly set `facilitatorFee`:

```typescript
{
  price: "$0.10",
  facilitatorFee: "$0.02",  // Fixed fee
}
```

---

## Multi-Network Support

```typescript
// Accept payments on multiple networks
app.post(
  "/api/multi-network",
  paymentMiddleware("0xYourAddress", {
    price: "$1.00",
    network: ["base-sepolia", "base"], // Multiple networks
  }),
  (req, res) => {
    const { network } = req.x402!;
    res.json({ message: `Paid on ${network}` });
  },
);
```

---

## Multiple Routes Configuration

```typescript
// Protect multiple routes with different prices
app.use(
  paymentMiddleware(
    "0xYourAddress",
    {
      "/api/basic": {
        price: "$0.01",
        network: "base-sepolia",
      },
      "/api/premium": {
        price: "$1.00",
        network: ["base-sepolia", "base"],
      },
      "/api/enterprise": {
        price: "$10.00",
        network: "base",
        facilitatorFee: "$0.50",
      },
    },
    { url: "https://facilitator.x402x.dev" },
  ),
);

// Route handlers can access req.x402
app.get("/api/basic", (req, res) => {
  const { payer } = req.x402!;
  res.json({ message: "Basic access", payer });
});
```

---

## Custom Settlement Hooks

```typescript
// Use TransferHook for revenue split (built-in)
import { TransferHook } from "@secured-finance/x402-core";

app.post(
  "/api/referral",
  paymentMiddleware("0xMerchantAddress", {
    price: "$0.10",
    network: "base-sepolia",
    hook: TransferHook.getAddress("base-sepolia"),
    hookData: TransferHook.encode([
      { recipient: "0xReferrerAddress", bips: 2000 }, // 20% to referrer
      { recipient: "0xPlatformAddress", bips: 1000 }, // 10% to platform
      // Merchant gets remaining 70%
    ]),
  }),
  (req, res) => {
    res.json({ message: "Revenue split executed" });
  },
);
```

---

## X402Context Access

The middleware extends Express `Request` with an `x402` property containing payment details:

```typescript
import type { X402Request } from '@secured-finance/x402-express';

app.post('/api/payment',
  paymentMiddleware(...),
  (req: X402Request, res) => {
    const x402 = req.x402!;

    // Access verified payment information
    console.log("Payer:", x402.payer);              // Address of payer
    console.log("Amount:", x402.amount);            // Amount in atomic units
    console.log("Network:", x402.network);          // Network used
    console.log("Payment:", x402.payment);          // Full payment payload
    console.log("Requirements:", x402.requirements); // Payment requirements

    // Settlement information (x402x specific)
    if (x402.settlement) {
      console.log("Router:", x402.settlement.router);
      console.log("Hook:", x402.settlement.hook);
      console.log("Hook Data:", x402.settlement.hookData);
      console.log("Facilitator Fee:", x402.settlement.facilitatorFee);
    }

    res.json({ success: true });
  }
);
```

---

## API Reference

### `paymentMiddleware(payTo, routes, facilitator?)`

Creates Express middleware for x402x payment processing.

**Parameters:**

- `payTo: string` - Final recipient address for payments
- `routes: X402xRoutesConfig` - Route configuration(s)
- `facilitator?: FacilitatorConfig` - Optional facilitator configuration

**Returns:** Express middleware function

### `X402xRouteConfig`

```typescript
interface X402xRouteConfig {
  price: string | Money; // USD or Money object
  network: Network | Network[]; // Single or multiple networks
  hook?: string | ((network) => string);
  hookData?: string | ((network) => string);
  facilitatorFee?: "auto" | string | Money | ((network) => string | Money);
  maxFeePercentage?: number; // Max fee as percentage of payment (0-1, default: 0.1)
  config?: {
    description?: string;
    mimeType?: string;
    maxTimeoutSeconds?: number;
    resource?: Resource;
    errorMessages?: {
      paymentRequired?: string;
      invalidPayment?: string;
      noMatchingRequirements?: string;
      verificationFailed?: string;
      settlementFailed?: string;
    };
  };
}
```

### `X402Context`

```typescript
interface X402Context {
  payer: Address | SolanaAddress; // Verified payer address
  amount: string; // Payment amount (atomic units)
  network: Network; // Payment network
  payment: PaymentPayload; // Decoded payment
  requirements: PaymentRequirements; // Matched requirements
  settlement?: {
    // x402x settlement info
    router: Address;
    hook: Address;
    hookData: string;
    facilitatorFee: string;
  };
}
```

---

## Payment Flow

1. Returns 402 with payment requirements when no payment is provided
2. Decodes `X-PAYMENT` header from client
3. Verifies payment signature via facilitator
4. Attaches payment details to `req.x402`
5. Runs your route handler
6. Settles payment via facilitator (if response status < 400)
7. Returns `X-PAYMENT-RESPONSE` header to client

---

## Related Packages

- [`@secured-finance/x402-core`](core.md) - Core utilities and types
- [`@secured-finance/x402-hono`](hono.md) - Hono middleware (alternative to Express)
- [`@secured-finance/x402-fetch`](fetch.md) - Client-side fetch wrapper
- [`@secured-finance/x402-react`](react.md) - React hooks for payments

---

## Next Steps

- **[Quick Start Guide](../quick-start.md)** - Complete tutorial
- **[Network Guide](../guides/network-guide.md)** - Network details and contracts
- **[Core Package](core.md)** - Advanced usage and utilities
- **[Facilitator Guide](../guides/facilitator-guide.md)** - Build your own facilitator
