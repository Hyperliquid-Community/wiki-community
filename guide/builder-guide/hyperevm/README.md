---
icon: laptop-code
---

# HyperEVM

The **HyperEVM** empowers developers to create any type of decentralized application while seamlessly interacting with **Hyperliquid’s native L1 components**.

This section serves as a **practical,** step-by-step guide for anyone looking to **build and deploy dApps** on **Hyperliquid**. From setting up an **EVM environment** to integrating **unique HyperCore functionalities**, you’ll find everything you need here to get started.

1. **EVM Basics**\
   Learn how to work with the standard EVM features and tools on Hyperliquid:
   * **RPC Nodes & Endpoints**: Discover the available RPC endpoints for interacting with the network.
   * **Block Explorers & Analysis Tools**: Track transactions, verify contracts, and analyze on-chain activity.
   * **Main Contract Addresses**: Access key deployed contracts.
   * **dApp Setup & Deployment**: Configure your app, integrate wallets (Wagmi, WalletConnect), and deploy contracts (Foundry, Hardhat).
2. **HyperEVM Specificities**
   * **Dual-Block Architecture**: Fast, frequent _Small Blocks_ plus slower, high-throughput _Large Blocks_—all under one EVM chain.
   * **Native Transfers**: Move spot assets between the HyperCore and HyperEVM to leverage the best of both worlds.
   * **Interacting with the** HyperCore: Access Hyperliquid’s core functionality via Read/Write Precompiles.
   * **Additional Helpers**:
     * _Indexing the HyperEVM_: Retrieve raw HyperEVM block data without running your own node.
     * _Wrapped Hype_: An immutable contract modeled after wrapped ETH, enabling streamlined asset interactions.

#### **Resources**

* 📖 [HyperEVM Explanation](../../../architecture/hyperevm.md) → High-level overview of [HyperEVM](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm/tools-for-hyperevm-builders) and access to the [official documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm).
* 💧 **Testnet Tokens:**
  * [Hyperlend Faucet](https://testnet.hyperlend.finance/dashboard) → Get **HYPE** & **MBTC**.
  * [Hypurr.fi Faucet](https://app.hypurr.fi/faucet) → Get **sUSDe, USDC, SolvBTC, HYPE**.
  * [Hyperliquid Testnet Faucet](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/testnet-faucet) → Claim **USDC**.
    * **Native Transfers:** Buy **HYPE** with **USDC** and send it to **`0x22...22`** → [More Info](specificities.md#id-1.-native-transfers).
* ⚡ [Asset Management](../../../ecosystem/projects/tools.md#blockchain-explorers)
* Setting up your RPC endpoint with [@HypeRPC](https://x.com/hyperpc_/status/1919334165092376829)

{% hint style="success" %}
**Stay Updated:** Check pinned messages in <kbd>#builders</kbd> Discord channel. If you have **questions**, that’s the best place to ask!
{% endhint %}
