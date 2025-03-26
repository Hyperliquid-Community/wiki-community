---
icon: laptop-code
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

# dApps (EVM)

The **HyperEVM** empowers developers to create any type of decentralized application while seamlessly interacting with **Hyperliquid’s native L1 components**.

This section serves as a **practical,** step-by-step guide for anyone looking to **build and deploy dApps** on **Hyperliquid**. From setting up an **EVM environment** to integrating **unique L1 functionalities**, you’ll find everything you need here to get started.

1. **EVM Basics**\
   Learn how to work with the standard EVM features and tools on Hyperliquid:
   * **RPC Nodes & Endpoints**: Discover the available RPC endpoints for interacting with the network.
   * **Block Explorers & Analysis Tools**: Track transactions, verify contracts, and analyze on-chain activity.
   * **Main Contract Addresses**: Access key deployed contracts.
   * **dApp Setup & Deployment**: Configure your app, integrate wallets (Wagmi, WalletConnect), and deploy contracts (Foundry, Hardhat).
2. **HyperEVM Specificities**
   * **Native Transfers**: Move spot assets between the L1 and HyperEVM to leverage the best of both worlds.
   * **Dual-Block Architecture**: Fast, frequent _Small Blocks_ plus slower, high-throughput _Large Blocks_—all under one EVM chain.
   * **Interacting with the L1**: Access Hyperliquid’s core functionality via Read/Write Precompiles.
   * **Additional Helpers**:
     * _Indexing the HyperEVM_: Retrieve raw HyperEVM block data without running your own node.
     * _Wrapped Hype_: An immutable contract modeled after wrapped ETH, enabling streamlined asset interactions.

#### **Resources**

* 📖 [HyperEVM Explanation](../../../technology-breakdown/hyperevm.md) → High-level overview of HyperEVM and access to the [official documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/evm).
* 💧 **Testnet Tokens:**
  * [Hyperlend Faucet](https://testnet.hyperlend.finance/dashboard) → Get **HYPE** & **MBTC**.
  * [Hypurr.fi Faucet](https://app.hypurr.fi/faucet) → Get **sUSDe, USDC, SolvBTC, HYPE**.
  * [Hyperliquid Testnet Faucet](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/testnet-faucet) → Claim **USDC**.
    * **Native Transfers:** Buy **HYPE** with **USDC** and send it to **`0x22...22`** → [More Info](hyperevm-specificities.md#id-1.-native-transfers).
* ⚡ **Asset Management:**
  * [HyperEdge Dashboard (Testnet)](https://hyperedge-testnet.vercel.app) → Easily Visualize & manage assets across **EVM, Spot, and Perp**.
  * [HyperEdge Dashboard (Mainnet)](https://app.hyperedge.finance) → Same on mainnet.

{% hint style="success" %}
**Stay Updated:** Check pinned messages in <kbd>#builders</kbd> Discord channel. If you have **questions**, that’s the best place to ask!
{% endhint %}
