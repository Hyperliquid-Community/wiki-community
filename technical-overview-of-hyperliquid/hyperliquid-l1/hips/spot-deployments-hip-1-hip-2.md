---
icon: person-walking-luggage
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Spot Deployments (HIP-1/HIP-2)

## HIP-1: Native Token Standard

### **What is HIP-1?**

HIP-1 defines a **capped-supply, fungible token standard** native to Hyperliquid L1. When you deploy a HIP-1 token, you also get a built-in on-chain spot order book. This order book allows trading directly against **Spot USDC**—the chain’s primary quote asset.

### **Key Features:**

* **Customizable Token Parameters:**
  * **Name & Decimals:** Human-readable names (up to 6 chars) and flexible decimal settings (e.g., “weiDecimals” and “szDecimals” to control precision).
  * **Max Supply:** Define a fixed initial supply that can decrease over time (e.g., due to trading fees or potential burns).
  * **Initial Distribution:** Assign initial balances to selected addresses or proportional allocations to holders of another HIP-1 token (anchors).
* **Native Spot Order Book Integration:**\
  Every HIP-1 token comes with its own on-chain order book paired with Spot USDC, enabling immediate, permissionless trading without the need to build separate infrastructure.
* **Future EVM Compatibility:** Once the HyperEVM is live, a deployed HIP-1 token can be linked to a corresponding ERC-20 contract on the EVM side.
* **Gas & Deployment Costs:**\
  Deployment is governed by a **31-hour Dutch auction** that sets the “gas cost” of bringing a new HIP-1 token to market. Costs are initially denominated in USDC and will eventually transition to the native Hyperliquid token.
* **Trading & Fees:**\
  Spot trading fees mirror the platform’s existing fee schedule. Non-USDC fees currently burn the collected tokens, though future upgrades might redirect these fees to liquidity providers or token stakers.
* **Dusting Mechanism:**\
  Very small (“dust”) balances are periodically aggregated and either sold on the open market or burned if too small. This ensures a cleaner user experience and helps tidy up negligible holdings.

**In Short:**\
HIP-1 makes it simple to **create a new token** with built-in trading mechanics—no separate smart contracts or custom solutions required. You get transparent on-chain markets from the start.

***

## HIP-2: Hyperliquidity

### **What is HIP-2?**

HIP-2 introduces **Hyperliquidity**, a decentralized liquidity strategy that automatically provides consistent buy and sell orders at tight spreads. Think of it like a built-in market maker: always on, fully on-chain, and secured by the same Layer 1 consensus that runs the order books.

### **Key Features:**

* **Liquidity Bootstrapping:**\
  New tokens often struggle to find stable liquidity early on. Hyperliquidity ensures that from day one, there’s a structured range of orders, making price discovery smoother and more efficient.
* **Parameters & Customization:**\
  Deployers set parameters like the starting price, order size, and number of orders. Hyperliquidity then maintains a 0.3% spread and updates every \~3 seconds, automatically adjusting orders based on the token’s available balance.
* **No External Operators:**\
  Unlike centralized or smart-contract-based market makers, Hyperliquidity requires no third-party intervention. It’s baked directly into the protocol, ensuring continuous and transparent liquidity provision.
  * **Locked Liquidity for a Reliable Baseline:** Other users, can contribute liquidity directly to Hyperliquidity by funding its range. This liquidity is permanently locked within the defined price range, providing a stable and predictable foundation for the market.
  * **User-Driven Limit Orders (e.g., MM):** Beyond locked liquidity, individual users can place limit orders directly on the order book. These orders are not locked and can be adjusted or removed at any time.

**In Short:**\
HIP-2 democratizes liquidity provision. By ensuring that every HIP-1 token can access continuous and reliable liquidity, it significantly reduces the friction of launching a new token and helps foster active, healthy markets.

***

#### Additional Resources & Guides:

* For a practical, **step-by-step guide** on how to deploy and manage your token, please refer to the [Community Docs’ “Spot Deployments” section](https://community-hyperliquid.gitbook.io/community-docs/for-builders-or-traders/spot-deployments). This resource provides concrete instructions and best practices for real-world deployment.
* The information here is drawn from the official Hyperliquid documentation ([HIPs section](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips)) as well as community insights and discussions shared on social media (such as [these tweets](https://x.com/KingJulianIAm/status/1813397274237546499)).
