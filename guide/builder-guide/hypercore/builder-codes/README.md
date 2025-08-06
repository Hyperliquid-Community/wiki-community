---
icon: browsers
---

# Builder Codes

This page guides you through setting up and customizing **Builder Codes** using a boilerplate **template** provided by [@SovrunOfficial](https://x.com/SovrunOfficial). We’ll walk through **recreating** the Next.js framework and **restructuring** the app’s API calls with the [Unofficial TypeScript SDK](https://github.com/nomeida/hyperliquid/tree/main) for cleaner, more maintainable code. This foundation will make it easy to add any additional features you need.

> **Alternative:** If you prefer Rust, there's also **Ferrofluid** - a high-performance Rust SDK for Hyperliquid available. Check it out [here](https://x.com/controlcthenv/status/1937253831416635483).

### Template Features

* **Secure Wallet Connection (via AppKit)**\
  Quickly connect user wallets, enhancing both convenience and security.
* **Spot Trading Interface**\
  Provides straightforward buy/sell functionality for tokens on Hyperliquid L1.
* **Builder Fee Approval System**\
  Allows builders to include and manage custom fees on top of Hyperliquid’s fees.
* **Agent-Based Trading System**\
  Enhances security by delegating order placement to an “agent.” This agent can only execute trades and cannot move user funds, reducing the risk of unauthorized withdrawals.
* **Modern UI**\
  Built with Tailwind CSS and shadcn/ui, providing a sleek, responsive design that’s easy to customize.
* **Real-Time Price and Balance Updates**\
  Displays current market data and user balances.

***

### Tech Stack

* **Framework**: **Next.js 15**\
  A popular React-based framework that offers server-side rendering, file-based routing, and powerful optimizations.
* **Language**: **TypeScript**\
  Ensures type safety and better maintainability, especially helpful for Web3 and blockchain integrations.
* **Styling**: **Tailwind CSS**\
  Provides utility-first classes for rapid UI development and consistent design patterns.
* **UI Components**: **shadcn/ui**\
  Delivers a modular, customizable component library that pairs seamlessly with Tailwind.
* **Web3 Libraries**: **Wagmi, Viem, Ethers.js**\
  Facilitates wallet connections, contract interactions, and transaction handling on Hyperliquid L1.
* **State Management**: **Zustand**\
  A lightweight, intuitive library for managing global state in your application.
* **Data Fetching**: **TanStack Query**\
  Handles data fetching and caching, making real-time updates more efficient.
* **Package Manager**: **pnpm** or **npm**\
  Choose **pnpm** for faster installs and disk efficiency or stick with **npm** if it's more familiar.

***

### Roadmap

1. **Set Up Sovrun’s Template**
   * **Clone the boilerplate repository** or **follow the guide to rebuild it from scratch** for a deeper understanding.
   * Verify that wallet connection, basic trading, and UI components are functioning.
2. **Replace API Calls with the Hyperliquid TypeScript SDK**
   * Reference our [API Endpoints Page](../endpoints/) to understand available methods.
   * Modify Sovrun’s structure to align with the approach used in the Typescript SDK for cleaner and more efficient API interactions.
3. **Customize Your Application**
   * Add or modify features to align with your project’s goals—think advanced trading strategies, analytics dashboards, or additional DeFi functionalities.

***

### Technical Explanation for Builders

**API Integration:**

* Query approved fees: `{"type": "maxBuilderFee", "user": "0x...", "builder": "0x..."}`
* Check earnings: `{"type": "referral", "user": "0x..."}`
* Access trade data: `https://stats-data.hyperliquid.xyz/Mainnet/builder_fills/{builder_address}/{YYYYMMDD}.csv.lz4`

**Key Implementation Notes:**

* URLs are **case-sensitive** with lowercase addresses required
* Example code in [Python SDK](https://github.com/hyperliquid-dex/hyperliquid-python-sdk/blob/master/examples/basic_builder_fee.py)
* Builder parameter: `f` value in **tenths of basis points** (10 = 1 basis point)

**Getting Started:**

* Review [API documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes)
* Test integration with small fees first
