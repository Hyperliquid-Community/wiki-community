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

_**Note:** The official HyperEVM documentation is not yet released. The HyperEVM is currently operating on a **testnet** environment, and its features, interfaces, and functionalities may change over time. The information here is based on early-stage materials and proof-of-concept implementations. We encourage developers to treat this as a preliminary guide and to stay tuned for future official updates._

This documentation draws heavily on insights and research shared by **Ambit Labs** in their article:\
[The Not-So-Definitive Guide to Hyperliquid Precompiles](https://medium.com/@ambitlabs/the-not-so-definitive-guide-to-hyperliquid-precompiles-f0b6025bb4a3). For a more detailed and technical explanation, we encourage you to read their original guide.

***

### Overview

**HyperEVM** is part of the Hyperliquid L1 blockchain, integrated directly into the same consensus layer (HyperBFT) that secures the L1. Unlike most EVM implementations that sit on separate networks, the HyperEVM is built _within_ the Hyperliquid ecosystem. This design enables seamless interactions between smart contracts and Hyperliquid’s core features—most notably the on-chain **spot and perp order books**.

**Key innovation:** On HyperEVM, a smart contract can interact with the L1 order book just as it would with any native asset or function. This bridges the gap between traditional decentralized exchanges and on-chain programmability, offering a new paradigm for DeFi development. Imagine being able to directly integrate order book liquidity and execution into your EVM contracts without relying on external bridges or off-chain solutions.

#### **What does this mean for you as a developer?**

* Access deep liquidity on-chain without intermediaries.
* Deploy EVM contracts that can read **and** influence real-time trading conditions.
* Build new types of DeFi primitives that combine the flexibility of smart contracts with robust, natively integrated order book markets.

***

### Hyperliquid Stack: L1 + EVM

* **Hyperliquid L1:** A high-performance, permissioned chain that runs native spot and perp order books. It achieves faster block times tailored for order execution and liquidity maintenance.
* **HyperEVM:** A general-purpose, **EVM-compatible** environment running under the same consensus. It’s permissionless—anyone can deploy smart contracts here. These contracts can read data and send actions to the L1.

**Execution model:** The L1 and the EVM run sequentially. The EVM can read the L1’s state from the previous block and submit actions to be included in the subsequent L1 block. This ordering provides a predictable cycle of read-then-write across the two environments.

***

### Interacting with the L1 from the HyperEVM

#### Reading L1 State with Precompiles

**Precompiles** are special addresses that provide read-access to L1 data directly from within the EVM. From a developer’s perspective, they function like contracts at known addresses, but internally, they give you direct hooks into L1 state.

**Example Use Case:** Retrieve a user’s perp position or spot balance from the L1 order books during the EVM execution. Precompiles ensure that your contract’s logic can be informed by live market data—no extra oracle or off-chain computation needed.

#### Writing to the L1 with Events

To send **actions** (like placing or canceling orders) from an EVM contract to the L1, you emit **events** from a special system contract address (`0x333...3333`). These events are transformed into actual L1 transactions in the next L1 block.

**Key Points:**

* Actions are not executed atomically with your EVM transaction. They occur subsequently, meaning you can’t get immediate confirmation or updated state within the same EVM block.
* If an action (like placing an order) fails on the L1, your EVM transaction still remains executed as is. This partial atomicity should be carefully considered when designing protocols.

***

### Important Considerations

1. **Partial Atomicity:**\
   While the EVM transaction and event emission are atomic (if the EVM transaction reverts, no event is emitted), the **execution of L1 actions triggered by those events occurs later** and may fail independently.
2. **Account Initialization:**\
   Before a contract can interact effectively with the L1, it must have an L1 account. This is done by depositing a “dust” amount of a native or linked asset into the smart contract’s address on the L1, ensuring the account is recognized on-chain.
3. **Balance Tracking:**\
   Transferring tokens to the L1 system address (`0x222...2222`) updates L1 balances in the subsequent block. Until then, there’s a brief “pre-crediting” period where balances don’t appear on either chain’s standard queries. Protocols interacting with L1/EVM balances must account for this delay.
4. **Message Sender vs. Origin:**\
   Actions initiated by an EVM contract appear on the L1 as if performed by the **contract itself**, not the original user. Ensure your smart contract logic provides ways to close positions or recover funds, as the L1 may attribute these actions to the contract’s address
