---
description: X402 packages for server-side payment integration
---

# 📦 Packages

X402 provides specialized packages for different server frameworks and use cases. Choose the package that matches your stack.

---

## Available Packages

### [@secured-finance/sf-x402](core.md) - Core Library
**For**: Building facilitators, custom integrations

The core package provides low-level functions for payment verification and settlement. Use this if you're building a facilitator service or need direct access to the protocol.

**Key Functions:**
- `verify()` - Verify payment signatures
- `settle()` - Settle payments on-chain
- `getSupportedKinds()` - List supported payment types

[**View Core Package Documentation →**](core.md)

---

### [@secured-finance/sf-x402-express](express.md) - Express Middleware
**For**: Express.js applications

Drop-in Express middleware that handles payment verification and 402 responses automatically. Add paid endpoints with just 3 lines of code.

**Features:**
- Drop-in middleware (3 lines of code)
- Dynamic pricing support
- Transaction tracking
- TypeScript support

[**View Express Documentation →**](express.md)

---

### [@secured-finance/sf-x402-next](next.md) - Next.js Middleware
**For**: Next.js applications (App Router & Pages Router)

Next.js middleware for payment-gated API routes and server actions. Works with both App Router and Pages Router.

**Features:**
- Edge runtime compatible
- Paywall HTML support
- Coinbase Onramp integration (optional)
- Session token API

[**View Next.js Documentation →**](next.md)

---

## Quick Comparison

| Feature | Core | Express | Next.js |
|---------|------|---------|---------|
| **Use Case** | Build facilitators | Express apps | Next.js apps |
| **Complexity** | Low-level | High-level | High-level |
| **Integration** | Manual | 3 lines of code | Middleware |
| **Paywall** | No | Yes | Yes |
| **Coinbase Onramp** | No | Yes | Yes |

---

## Installation

```bash
# Core package (for facilitators)
pnpm add @secured-finance/sf-x402

# Express middleware
pnpm add @secured-finance/sf-x402-express

# Next.js middleware
pnpm add @secured-finance/sf-x402-next
```

---

## Need Help?

* [🚀 Quick Start Guide](../quick-start.md) - Get started in 10 minutes
* [📖 Network Guide](../guides/network-guide.md) - Choose the right network
* [💡 Use Cases](../guides/use-cases.md) - Real-world examples
* [🏦 Facilitator Guide](../guides/facilitator-guide.md) - Build your own facilitator
