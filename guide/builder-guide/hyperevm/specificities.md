---
icon: sparkles
---

# Specificities

This guide covers the essential technical components and considerations for developers building on HyperEVM. For conceptual understanding, see our [HyperEVM Overview](../../../architecture/hyperevm.md).&#x20;

### Important Technical Considerations

Before diving into specific features, developers should understand these critical aspects of HyperEVM:

* **Partial Atomicity**: Actions from HyperEVM to HyperCore occur in subsequent blocks, your EVM transaction succeeds immediately, but the HyperCore actions it triggers might fail independently.
* **Account Initialization**: Smart contracts cannot interact with HyperCore until they have a corresponding HyperCore account. Initialize by sending a small ("dust") amount of any asset to the contract address on HyperCore.
* **Balance Tracking**: When transferring assets between environments, a brief "pre-crediting" period exists where balances may not appear in standard queries until the next block.
* **Message Origin**: HyperCore sees actions from smart contracts as originating from the contract itself, not the end user. Design your contracts with recovery mechanisms to handle this.

***

#### 1. Native Transfers

Move spot assets between Hyperliquid’s L1 (“native spot”) and the EVM (“EVM spot”). After **linking** an ERC20 contract to a native asset, you can **deposit** and **withdraw** simply by transferring tokens to the system address (`0x20...`).

* **Setup**: Use a `setEvmContract` action to bind the native spot asset with its EVM counterpart.
* **Supply**: Ensure the system address holds the full amount of the asset on the “other side.”
* **HYPE**: Functions as the **native gas token** on the EVM; special handling is required for deposits/withdrawals.

For detailed instructions, see the [Official Docs on Native Transfers](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/evm/native-transfers).

***

#### 2. Dual-Block Architecture

HyperEVM splits throughput into **small blocks** (fast, lower gas limit) and **large blocks** (slower, higher gas limit). Both block types share a single, ever-increasing block number sequence.

* **Small Blocks**
  * Fast confirmations (\~2s per block)
  * Gas limit: 2M
  * Ideal for frequent transactions and real-time interactions.
* **Large Blocks**
  * Slower execution (\~1 min per block)
  * High gas limit: 30M
  * Designed for complex contract deployments and bulk transactions.

Switching between block types can be done via an L1 action (e.g., setting `usingBigBlocks: true`). For a deeper dive, consult the [Official Docs on Dual-Block Architecture](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/evm/dual-block-architecture). You can also use this [mainnet frontend tool](https://hyperevm-block-toggle.vercel.app/) to toggle block types directly.

***

#### 3. Interacting with the L1 (Read/Write Precompiles)

Hyperliquid provides **read** and **write** precompiles to directly access L1 functions without cross-chain complexity.

* **Read Precompiles**
  * **Addresses**: Start at `0x0000000000000000000000000000000000000800`.
  * **Capabilities**: Query perps positions, spot balances, vault equity, staking delegations, oracle prices, and L1 block numbers.
  * **Sync**: Always reflects the latest L1 state at EVM block construction.
* **Write Precompile**
  * **Address**: `0x3333333333333333333333333333333333333333`.
  * **Actions**: Supports placing IOC orders, transferring assets between vaults or perps, staking, and spot sends—directly from the EVM.

For code samples and full method details, see the [L1 Integration Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/evm/interacting-with-the-l1).

***

#### 4. Additional Helpers

**4.1 Indexing the HyperEVM**

Retrieve raw HyperEVM block data from an **S3 bucket** (`s3://hl-testnet-evm-blocks/`) to build custom services like block explorers or analytics dashboards—no full node required. Files are stored in **MessagePack** format, compressed with **LZ4**, and named by EVM block number.

For more information, visit the [Indexing Guide](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/evm/raw-hyperevm-block-data).

**4.2 Wrapped Hype**

A canonical **Wrapped HYPE (WHYPE)** contract is deployed at `0x555...5`. It mirrors the standard wrapped-ETH design—immutable and lightweight—allowing HYPE to function as an **ERC-20** asset within the EVM.

Learn more in the [Wrapped HYPE Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/evm/wrapped-hype).

***

### Security Patterns - Trust Domain Matching

Understanding when to use precompiles versus external oracles is critical for building secure applications on HyperEVM:

#### Use Precompiles When:

* **Interacting with HyperCore only** - Trading, vault management, staking operations
* **Reading HyperCore state** - Positions, balances, internal prices, delegations
* **Submitting orders through CoreWriter** - Ensures state consistency with execution engine

#### Use External Oracles When:

* **External system integration** - Cross-chain bridges, external settlements
* **Real-world asset exposure** - BTC/USD prices for stablecoins, cross-exchange arbitrage
* **Non-Hyperliquid obligations** - External collateral, multi-chain protocols

#### Security Rule

If your contract uses **write precompiles** (CoreWriter) to interact with HyperCore, it should trust **read precompiles** for all related price and balance references to avoid state mismatches.

#### Key Principles

* **Precompiles anchor contracts inside Hyperliquid** - Use for internal system operations
* **Oracles anchor contracts to external economic reality** - Use for cross-chain or external obligations
* **Trust domain matching** - Ensure every part of your capital flow references the right source of truth

_For more details, read_ [_Building Safely on Hyperliquid_](https://x.com/emaverick90/status/1926966482765812056)_._
