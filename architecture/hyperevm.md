---
icon: puzzle-piece
---

# HyperEVM

HyperEVM transforms Hyperliquid into a **fully programmable financial system** by integrating smart contract capabilities directly with Hyperliquid's high-performance order books. This represents a paradigm shift for DeFi by combining the efficiency of centralized exchange order books with the programmability of smart contracts. For the first time, developers can build applications that directly tap into deep, high-performance liquidity without sacrificing decentralization or requiring complex bridging solutions.

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

* **Small Blocks**: Process every 1 seconds with a 2M gas limit, perfect for quick transactions
* **Large Blocks**: Process approximately every minute with a 30M gas limit, ideal for complex operations

Most blockchain systems force a compromise between speed and capacity, either fast blocks with limited space or larger blocks that take longer to process. HyperEVM solves this by maintaining two separate transaction queues that feed into different block types.

This design allows users to choose what matters most: traders can use small blocks for near-instant order confirmations, while developers can deploy complex contracts through large blocks without congesting the network.

_For implementation details and code examples, see the_ [_dual-block architecture documentation_](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/dual-block-architecture)_._

#### Asset Movement Between HyperCore and HyperEVM

Assets can move freely between environments without traditional bridging risks:

* Each spot asset on HyperCore can be linked to an ERC20 token on HyperEVM
* **HYPE** (the native token) serves as gas on HyperEVM and can be transferred between environments
* There are no wrapped tokens or IOUs, it's the same asset in both places

Traditional cross-chain solutions require wrapped tokens, trusted validators, or lengthy verification periods. HyperEVM eliminates these complexities since both environments share the same underlying consensus. This creates a seamless experience where assets maintain their identity and properties regardless of which environment they're used in.

The system uses special addresses (starting with `0x200`...) to handle these transfers, maintaining a unified asset layer across the platform.

**Transfer Timing:**

* **HyperCore to HyperEVM:** Transfers are queued until the next HyperEVM block
* **HyperEVM to HyperCore:** Transfers happen in the same L1 block, immediately after the HyperEVM block is built
* **Block Processing Order:** L1 block → EVM block → EVM=>Core transfers processed → CoreWriter actions processed

_For implementation details and code examples, see the_ [_documentation_](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/hypercore-less-than-greater-than-hyperevm-transfers)_._

#### Accessing HyperCore from Smart Contracts

The real power of HyperEVM comes from two key mechanisms that enable smart contracts to interact with HyperCore's exchange features:

**Read Precompiles**

Special contracts at addresses starting with `0x000...0800` allow smart contracts to query HyperCore data directly:

* **User data** - Positions, balances, and vault information
* **Market data** - Mark prices and oracle prices
* **Staking data** - Delegations and validator information
* **System data** - L1 block number and other core metrics

Think of these as direct data pipelines into the exchange, giving your contracts real-time market information without relying on external oracles or APIs.

**CoreWriter contract**

A system contract at address `0x333...3333` allows smart contracts to initiate actions on HyperCore:

* **Trading** - Place limit orders with various time-in-force options (ALO, GTC, IOC)
* **Order Management** - Cancel orders by order ID (oid) or client order ID (cloid)
* **Vault Management** - Programmatic deposits and withdrawals
* **API Wallet Management** - Add API wallets with custom names
* **Staking operations** - Delegate/undelegate tokens, deposit/withdraw stakes
* **Asset transfers** - Move spot tokens and USD between accounts/markets
* **Contract finalization** - Deploy and initialize EVM contracts with custom storage slots

This architecture transforms passive smart contracts into active market participants while maintaining HyperCore's security model through structured, predictable actions.&#x20;

_For implementation details and code examples, see the_ [_developer documentation_](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/hyperevm/interacting-with-hypercore)_._

### Advantages - What Can You Build?

**Real-Time System Awareness**

Precompiles enable **near-real-time awareness** inside Hyperliquid, eliminating traditional DeFi latency:

* **Instant collateral checks** - No oracle delays for margin calculations
* **Synchronized liquidations** - Real-time position monitoring and execution
* **Dynamic rebalancing** - Immediate response to market conditions
* **Trustless automation** - No external keepers or relayers required

**Applications Now Possible**

With these tools, developers can create applications that were previously difficult or impossible:

* **Lending Protocols** - Incorporate orderbook prices, trustless liquidations on HyperCore order books
* **Liquid Staking Tokens** - Entirely onchain with governance through HIP-3 assets, no multisig control
* **Tokenized Trading Vaults** - Real-time equity tracking and programmatic management (e.g., tokenized HLP)
* **Self-hedging Loans** - Automatically manage risk through perps trading
* **Options Protocols** - Automatic delta hedging with instant position adjustments
* **DEX Aggregators** - Instant route optimization through HyperCore liquidity
* **Yield Strategies** - Respond to funding rates and market conditions in real-time

### Current Status

HyperEVM is currently in [alpha stage](../introduction/roadmap/#hyperevm). While core functionality is available, some features are still being rolled out gradually to ensure system stability.

**Current Development Focus:**

* **Throughput improvements** - Increasing transaction processing capacity
* **Gas limit optimization** - Improving small block gas limits for better everyday user experience
* **Block switching UX** - Making transitions between small and big blocks more seamless
* **Infrastructure stability** - Addressing RPC reliability and node performance
* **Developer tooling** - Enhanced debugging and monitoring capabilities

**Key Considerations:**

* **Big blocks** are primarily designed for builders deploying contracts rather than everyday user transactions
* The architecture prioritizes **HyperCore stability** - ensuring trading performance remains unaffected - [Source](https://x.com/xulian_hl/status/1938276997739995543)

For developers looking to start building, see our [Builder Guide](../guide/builder-guide/hyperevm/) with detailed technical documentation and code examples.

[View current HyperEVM projects →](../ecosystem/projects/hypercore.md)

### Resources

* [HyperEVM Documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperevm)
* Precompiles Guide:
  * [Xulian's Precompile Explanation](https://x.com/xulian_hl/status/1919617689124794692) | [Hyperliquid examples](https://x.com/HyperliquidX/status/1947178777244803543)
  * [A Breakdown for Dummies](https://x.com/emaverick90/status/1919727174426284488) | [Enables Real Time Awareness](https://x.com/emaverick90/status/1924805040121815399) by Eduardo (Felix Protocol)
  * Explanatory videos by [Hyperdrive](https://x.com/hyperdrivedefi/status/1926820809659515225) and by [Harmonix](https://x.com/harmonixintern/status/1941425571088781752).
* [Precompile HyperCore → HyperEVM Direction](https://x.com/xulian_hl/status/1916711761769804169) - Note that smart contracts perform actions on HyperCore initiated from HyperEVM, not the reverse, as HyperCore has no general purpose smart contracts
