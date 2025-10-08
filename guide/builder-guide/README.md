---
icon: square-code
---

# Builder Guide

HyperFoundation is on a mission to make Hyperliquid the **“Amazon Web Services of liquidity”**—a neutral backend that empowers anyone to build innovative financial applications without worrying about the heavy lifting. By offering robust, plug-and-play infrastructure, Hyperliquid lets you focus on creating value and delivering top-notch products.

#### A World of Possibilities

The current flagship application on Hyperliquid is the **DEX developed by Hyperliquid Labs**, but that’s only one example of what’s possible. Whether you’re envisioning new trading tools, risk management platforms, or entirely novel financial products, **Hyperliquid’s infrastructure is yours to explore**. This is the essence of **Open Finance**: building, iterating, and launching whatever you can imagine—free from the usual constraints of traditional finance or single-purpose blockchains.

#### Three Core Components of Hyperliquid

1. **HyperCore Perp & Spot:**
   * These are the foundational markets of Hyperliquid, accessible via **API endpoints**.
   * Instead of interacting directly with the RPC, users interact with **permissionless API servers**, which relay requests to the network’s consensus RPC. This design ensures **better load balancing, DDoS protection, and a familiar experience**, similar to cex.
2. **HyperEVM:**
   * A **standard EVM** environment with added features that grant access to **L1 primitives**.
   * Development feels familiar (e.g., using RPC calls and typical EVM tooling), but you also benefit from enhanced functionalities unique to Hyperliquid.
3. **Node Operators:**
   * Anyone can **run a node** and participate in network consensus, helping secure the network.
   * This open participation model underpins the decentralization of Hyperliquid and ensures its long-term resilience.

### **Why Build on HyperLiquid?**

HyperLiquid offers a unique opportunity for developers by combining two execution environments under the same consensus algorithm:

1. **HyperLiquid's Rust VM** – This onchain exchange powers **Perps, Spot, and Vaults**, providing unmatched liquidity and performance.
2. **HyperEVM** – Designed for building **all types** of decentralized applications (Dapps). It **benefits** from HyperLiquid's existing **liquidity**, **user base**, and **distribution**, making it an ideal environment for teams to launch their projects.

**Top Opportunities for Builders**

HyperLiquid’s community and ecosystem create specific advantages for various DeFi and governance applications:

* **Liquid Staking** – HyperLiquid's PoS chain needs a token for validation. A liquid staking service for its loyal user base could become the fastest-growing protocol.
* **Perps Traders and Market Makers** – Leverage HyperLiquid’s liquidity for options AMMs, prediction markets, and cross-collateral margin solutions.
* **HLP Holders** – The TVL in HLP vaults offers opportunities for tokenization, secondary liquidity, and yield trading. Build leverage vaults or complex DeFi strategies tailored to HLP users.
* **Spot Traders** – With the spot ecosystem growing, new tools such as spot leverage and governance/vesting solutions will enhance user experience and market efficiency.
* [Explore Builder Codes opportunities →](../../architecture/hypercore/dex/clearinghouse/fees-builder-codes.md#builder-opportunities)

For a detailed breakdown of opportunities and ecosystem insights, check out the [original thread by @0xKrishb](https://x.com/0xkrishb/status/1839441024919417077).

With the resources in this Builder Guide, you’ll have everything you need to **create, innovate, and deploy** your own applications on Hyperliquid.

Ready to dive in? Let’s get started!
