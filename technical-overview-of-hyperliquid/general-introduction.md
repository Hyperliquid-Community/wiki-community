---
icon: book-open
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

# General Introduction

**Welcome to the core of Hyperliquid’s technology stack!** Here, we’ll provide both a high-level overview and a deeper technical dive into the blockchain, its consensus mechanism, and the native components that make Hyperliquid a high-performance and innovative ecosystem.

### High-Level Diagram

_Below is a conceptual diagram sourced from the **Hyperliquid Foundation**. This visual will help you understand how the pieces fit together:_

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Core Components

**HyperBFT Consensus:**

* A consensus algorithm that ensures network nodes agree on the current state of the blockchain.
* Currently, decentralization is limited, with all four known nodes operated by the Hyperliquid team. Over time, this must evolve to align better with Web3’s decentralization ethos.
* The codebase for the Hyperliquid L1 has not yet been publicly released, and details may evolve as the ecosystem matures.

#### Hyperliquid L1 - Native Component&#x73;**:**

* A custom, from-scratch Layer 1 blockchain designed to power Hyperliquid’s flagship application—its decentralized exchange (DEX).
* Aims to achieve **up to 200,000 transactions per second** and **latency under 1 second**, far surpassing traditional blockchain performance metrics.
* **Divided into four primary “blocks”:**
  1. **Native Order Book:**
     * A fully on-chain order book for **spot** and **perpetual trading**.
     * Enables **transparent execution** of trades with all orders, funding rates, and liquidations recorded on-chain.
     * Supports **zero gas fees** on order placement and **up to 50x leverage** for perps.
     * **Seamless User Experience:** One-click trading without constant wallet approvals, streamlining the trading process.
  2. **Oracles:**&#x20;
     * Integrated price feeds that provide reliable and accurate external market data.
     * Crucial for ensuring fair pricing in perpetual contracts and spot trading.
     * Designed for high-frequency updates to match the speed of the platform.
  3. **Vaults:**&#x20;
     * Includes mechanisms like the **HLP (Hyperliquid Liquidity Provider) tokens** and an **Insurance Fund (AF)** to protect against market volatility and liquidation risks.
     * Redistributes trading fees to liquidity providers as rewards, ensuring a robust incentive system.
  4. **Dutch Auctions (HIP-1 / HIP-2):**
     * A native auction mechanism introduced to optimize token launches and price discovery.
     * Built directly into the protocol for seamless integration with trading and liquidity features.

#### **HyperEVM:**&#x20;

* The HyperEVM layer enables users to build and deploy their own applications, launch tokens, and access all of these financial primitives in one unified environment.
* High performance, native financial components, and EVM compatibility make it possible to build apps that require all three: **performance**, **liquidity**, and **programmability** in one place.
