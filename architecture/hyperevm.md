---
icon: puzzle-piece
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

# HyperEVM

HyperEVM transforms Hyperliquid into a **fully programmable financial system** by integrating smart contract capabilities directly with Hyperliquid's high-performance order books. This represents a paradigm shift for DeFi by combining the efficiency of centralized exchange order books with the programmability of smart contracts. For the first time, developers can build applications that directly tap into deep, high-performance liquidity without sacrificing decentralization or requiring complex bridging solutions.

This innovation eliminates the traditional DeFi trade-offs between liquidity depth, execution speed, and programmability. Rather than relying on AMMs or fragmented liquidity pools, HyperEVM applications can leverage HyperCore's mature order book—bringing **CEX-like performance** to the world of decentralized finance.

### How It Works

HyperEVM is not a separate chain but an extension of Hyperliquid, where:

1. **HyperCore**: Handles all trading activities, staking, native multisigs, and core exchange functionality
2. **HyperEVM**: Provides the smart contract environment where developers can build custom applications

HyperEVM is based on the **Cancun EVM specification** (without blob transactions), ensuring compatibility with existing Ethereum tools and development practices while adding Hyperliquid-specific enhancements.

These components share the same consensus mechanism and operate sequentially, allowing:

* Smart contracts to **read** HyperCore state (balances, positions, prices) from the previous block
* Contracts to **write** actions to be executed in the following HyperCore block

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>We encourage you to <a href="https://medium.com/@ambitlabs/the-not-so-definitive-guide-to-hyperliquid-precompiles-f0b6025bb4a3">read</a> the insights and research shared by <strong>Ambit Labs</strong></p></figcaption></figure>

The following are HyperEVM's key differentiators:

#### Dual-Block Architecture

HyperEVM uses an innovative dual-block system to handle different transaction needs:

* **Small Blocks**: Process every \~2 seconds with a 2M gas limit, perfect for quick transactions
* **Large Blocks**: Process approximately every minute with a 30M gas limit, ideal for complex operations

Most blockchain systems force a compromise between speed and capacity, either fast blocks with limited space or larger blocks that take longer to process. HyperEVM solves this by maintaining two separate transaction queues that feed into different block types.

This design allows users to choose what matters most: traders can use small blocks for near-instant order confirmations, while developers can deploy complex contracts through large blocks without congesting the network.

#### Asset Movement Between HyperCore and HyperEVM

Assets can move freely between environments without traditional bridging risks:

* Each spot asset on HyperCore can be linked to an ERC20 token on HyperEVM
* HYPE (the native token) serves as gas on HyperEVM and can be transferred between environments
* There are no wrapped tokens or IOUs, it's the same asset in both places

Traditional cross-chain solutions require wrapped tokens, trusted validators, or lengthy verification periods. HyperEVM eliminates these complexities since both environments share the same underlying consensus. This creates a seamless experience where assets maintain their identity and properties regardless of which environment they're used in.

The system uses special addresses (starting with 0x200...) to handle these transfers, maintaining a unified asset layer across the platform.

#### Accessing HyperCore from Smart Contracts

The real power of HyperEVM comes from two key mechanisms that enable smart contracts to interact with HyperCore's exchange features:

**Read Precompiles**

Special contracts at addresses starting with 0x000...0800 let smart contracts query HyperCore data:

* User positions, balances, and vault information
* Mark prices and oracle data
* Staking information and delegations

Think of these as direct data pipelines into the exchange, giving your contracts real-time market information without relying on external oracles or APIs.

**Write System Contract**

A system contract at address 0x333...3333 allows smart contracts to initiate actions on HyperCore:

* Place immediate-or-cancel (IOC) orders
* Manage vaults and staking
* Transfer assets between different parts of the system

This capability transforms passive smart contracts into active market participants. For example, an options protocol could automatically hedge delta exposure by trading in the perpetuals market, or a yield strategy could dynamically adjust positions based on funding rates; all without requiring user intervention or trusted third parties.

Unlike arbitrary execution, these are structured actions that follow HyperCore's security model, ensuring that the core exchange functionality remains secure and predictable.

### What Can You Build?

With these tools, developers can create applications that were previously difficult or impossible:

* **Lending protocols** that liquidate directly into the spot order book
* **Self-hedging loans** that automatically manage risk through perps trading
* **Options protocols** with automatic delta hedging
* **Yield strategies** that respond to market conditions in real-time
* **Tokenized trading vaults** managing complex strategies
* **Liquid staking solutions** with programmable rewards distribution

### Current Status

HyperEVM is currently in [alpha stage](../introduction/roadmap/). While core functionality is available, some features are still being rolled out gradually to ensure system stability.

For developers looking to start building, see our [Builder Guide](../guide/builder-guide/hyperevm/) with detailed technical documentation and code examples.

### Resources

* [HyperEVM Documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm)
* Precompiles Guide:
  * [The Not-So-Definitive Guide to Hyperliquid Precompiles](https://medium.com/@ambitlabs/the-not-so-definitive-guide-to-hyperliquid-precompiles-f0b6025bb4a3) - First article explaining HyperEVM by Ambit Labs
  * [Xulian's Precompile Explanation](https://x.com/xulian_hl/status/1919617689124794692)
  * [A Breakdown for Dummies](https://x.com/emaverick90/status/1919727174426284488) by Eduardo (Felix Protocol)
* [Precompile HyperCore → HyperEVM Direction](https://x.com/xulian_hl/status/1916711761769804169) - Note that smart contracts perform actions on HyperCore initiated from HyperEVM, not the reverse, as HyperCore has no general purpose smart contracts
