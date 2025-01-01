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

# Overview

**Welcome to the core of Hyperliquid’s technology stack!** Here, we’ll provide both a high-level overview and a deeper technical dive into the blockchain, its consensus mechanism, and the native components that make Hyperliquid a high-performance and innovative ecosystem.

### High-Level Diagram

_Below is a conceptual diagram sourced from the **Hyperliquid Foundation**. This visual will help you understand how the pieces fit together:_

<figure><img src="../.gitbook/assets/Hyperliquid_Image_Foundation (2).jpg" alt=""><figcaption></figcaption></figure>

### Core Components

#### **HyperBFT Consensus:**

* A consensus algorithm that ensures network nodes agree on the current state of the blockchain.
* Currently, decentralization is limited, with all four known nodes operated by the Hyperliquid team. Over time, this must evolve to align better with Web3’s decentralization ethos.
* The codebase for the Hyperliquid L1 has not yet been publicly released, and details may evolve as the ecosystem matures.

#### Hyperliquid L1 - Native Component&#x73;**:**

A **custom, from-scratch Layer 1 blockchain** designed to power Hyperliquid’s flagship application—its decentralized exchange (DEX). It aims to achieve **up to 200,000 TPS** and **latency under 1 second**, far surpassing traditional blockchain performance metrics.

**Divided into Five Primary “Blocks”:**

1. **Native Order Book:**
   * **Fully On-Chain:** All orders, trades, funding rates, and liquidations are recorded transparently on-chain.
   * **Gas-Free Orders & Leverage:** Place orders without gas fees and access up to **50x leverage** on perpetuals.
   * **Seamless UX:** One-click trading without repeated wallet approvals for a streamlined experience.
2. **Clearinghouse**
   * **Core Exchange State Management:** The Clearinghouse manages all user states for both perpetual and spot trading.
   * **Perpetuals:** Handles cross-margin balances and positions, with optional isolated margin support to allocate specific collateral to individual positions, reducing risk exposure.
   * **Spot Trading:** Similarly manages token balances and holds for spot trading, ensuring accurate and efficient account states across the platform.
3. **Oracles:**&#x20;
   * **Accurate Market Data:** Integrated price feeds ensure reliable and fair pricing for both spot and perpetual markets.
   * **High-Frequency Updates:** Updated rapidly to match the speed and precision of Hyperliquid’s platform.
4. **Vaults:**&#x20;
   * **Liquidity & Protection:** Mechanisms like **HLP** (Hyperliquid Liquidity Provider) tokens and an **AF** (Assistance Fund) safeguard against volatility and liquidation risks.
   * **Fee Redistribution:** Trading fees are redistributed to liquidity providers, creating strong incentives for market participation.
5. **Spot Tokens (HIP-1 & HIP-2)**
   * **Easy Token Launches (HIP-1):** Deploy native spot tokens with a built-in on-chain order book for transparent, secure trading from day one.
   * **Integrated Liquidity (HIP-2):** Achieve “Hyperliquidity” with a mechanism inspired by Uniswap, tailored for order-book trading, ensuring dynamic and reliable liquidity for smoother price discovery.

#### **HyperEVM:**&#x20;

* The HyperEVM layer enables users to build and deploy their own applications, launch tokens, and access all of these financial primitives in one unified environment.
* High performance, native financial components, and EVM compatibility make it possible to build apps that require all three: **performance**, **liquidity**, and **programmability** in one place.
