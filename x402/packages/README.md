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

### [@secured-finance/sf-x402-express](middleware.md) & [@secured-finance/sf-x402-next](middleware.md) - Payment Middleware
**For**: Express.js and Next.js applications

Drop-in middleware for Express and Next.js that handles payment verification and 402 responses automatically. Add paid endpoints with just 3 lines of code.

**Features:**
- Simple integration (one line of middleware)
- Dynamic pricing support
- Multiple network support
- Custom paywall HTML
- TypeScript support

[**View Middleware Documentation →**](middleware.md)

---

## Quick Comparison

| Feature | Core | Middleware (Express/Next.js) |
|---------|------|------------------------------|
| **Use Case** | Build facilitators | Add payments to APIs |
| **Complexity** | Low-level | High-level |
| **Integration** | Manual | One line of code |
| **Paywall** | No | Yes |
| **Framework** | Any | Express.js, Next.js |

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
