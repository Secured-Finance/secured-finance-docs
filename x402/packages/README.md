---
description: X402 packages for server-side payment integration
---

# 📦 Packages

X402 provides specialized packages for different server frameworks and use cases. Choose the package that matches your stack.

---

## Available Packages

### [@secured-finance/x402-core](core.md) - Core Library
**For**: Building facilitators, custom integrations, and core utilities

The core package provides low-level functions for commitment calculation, network configuration, and facilitator API interactions. Use this if you're building a facilitator service or need direct access to the protocol.

**Key Functions:**
- `calculateCommitment()` - Calculate commitment hash for settlement parameters
- `getNetworkConfig()` - Get network configuration
- `addSettlementExtra()` - Add settlement extension to PaymentRequirements
- `verify()` - Verify payment signatures
- `settle()` - Settle payments on-chain
- `calculateFacilitatorFee()` - Calculate facilitator fees

[**View Core Package Documentation →**](core.md)

---

### [@secured-finance/x402-express](express.md) - Express Middleware
**For**: Express.js applications

Drop-in middleware for Express.js that handles payment verification and 402 responses automatically with x402x settlement support.

**Features:**
- Full x402 payment flow with settlement extensions
- X402Context extension for accessing payment details
- Multi-network support
- Dynamic facilitator fee calculation
- Custom settlement hooks

[**View Express Middleware Documentation →**](express.md)

---

### [@secured-finance/x402-hono](hono.md) - Hono Middleware
**For**: Hono applications (Cloudflare Workers, Edge Runtime)

Drop-in middleware for Hono that handles payment verification and 402 responses with x402x settlement support. Perfect for edge runtime environments.

**Features:**
- Drop-in middleware for Hono routes
- Automatic settlement mode support
- Dynamic facilitator fee calculation
- Edge runtime compatible
- Built-in caching for fee calculations

[**View Hono Middleware Documentation →**](hono.md)

---

### [@secured-finance/x402-client](client.md) - Client SDK
**For**: Client-side applications (React, Vue, vanilla JS)

Client SDK for x402x Serverless Mode - Execute on-chain contracts directly via facilitator without needing a resource server.

**Features:**
- Serverless mode - No backend needed
- React hooks included (useX402Client, useExecute)
- Automatic fee calculation
- Type-safe with comprehensive error handling

[**View Client SDK Documentation →**](client.md)

---

### [@secured-finance/x402-fetch](fetch.md) - Fetch Wrapper
**For**: Client-side fetch API integration

Fetch wrapper that automatically handles 402 Payment Required responses with settlement mode support.

**Features:**
- Automatic 402 response handling
- Commitment-based nonce for settlement mode
- Falls back to standard x402 for non-settlement payments
- Configurable maximum payment amount

[**View Fetch Wrapper Documentation →**](fetch.md)

---

### [@secured-finance/x402-react](react.md) - React Hooks
**For**: React applications

React hooks for the x402x settlement framework with wagmi integration.

**Features:**
- React hooks for payment flows
- Automatic mode detection
- Wagmi integration
- TypeScript support

[**View React Hooks Documentation →**](react.md)

---

## Quick Comparison

| Feature | Core | Express | Hono | Client | Fetch | React |
|---------|------|---------|------|--------|-------|-------|
| **Use Case** | Facilitators | Express APIs | Hono APIs | Client apps | Fetch wrapper | React apps |
| **Complexity** | Low-level | High-level | High-level | High-level | Medium | High-level |
| **Framework** | Any | Express.js | Hono | Any | Any | React |
| **Edge Runtime** | Yes | No | Yes | Yes | Yes | No |

---

## Installation

```bash
# Core package
npm install @secured-finance/x402-core

# Express middleware
npm install @secured-finance/x402-express

# Hono middleware
npm install @secured-finance/x402-hono @secured-finance/x402-core

# Client SDK
npm install @secured-finance/x402-client @secured-finance/x402-core

# Fetch wrapper
npm install @secured-finance/x402-fetch @secured-finance/x402-core

# React hooks
npm install @secured-finance/x402-react @secured-finance/x402-core
```

---

## Need Help?

* [🚀 Quick Start Guide](../quick-start.md) - Get started in 10 minutes
* [📖 Network Guide](../guides/network-guide.md) - Choose the right network
* [💡 Use Cases](../guides/use-cases.md) - Real-world examples
* [🏦 Facilitator Guide](../guides/facilitator-guide.md) - Build your own facilitator
