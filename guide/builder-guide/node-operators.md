---
icon: server
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

# Node Operators

_**Note:** This page is under active construction, and the information here may evolve as we learn more. Please check back for updates._

⚠️ **To stay informed, please refer to the pinned messages in the `#node-operators` Discord channel.** You’ll find the most current instructions, updates, and community-driven resources there.

***

### Overview

**Validators** play a crucial role in the Hyperliquid network by validating transactions, producing blocks, and securing the blockchain. Their performance can vary based on factors like **uptime**, the **quality and frequency of block proposals**, and adherence to network rules (i.e., avoiding **slashing events**). As the network matures, validators and node operators will have more tools, metrics, and best practices at their disposal.

**Non-Validating Nodes** help by providing additional services such as accessing data, supporting EVM functionality, or contributing to the network’s overall resilience without participating directly in block production.

***

### Latest Updates & Instructions

*   **EVM Support:**\
    A new `hl-visor` release supports EVM RPC. Once downloaded, run:

    <pre class="language-bash"><code class="lang-bash"><strong>curl https://binaries.hyperliquid.xyz/Testnet/hl-visor > hl-visor
    </strong>./hl-visor run-non-validator --serve-eth-rpc
    </code></pre>

    You can then query the EVM at `http://localhost:3001/evm`.
* **Permissionless Validators on Testnet:**\
  The validator set is now fully permissionless.
  * Self-delegate **10k HYPE** to register or stay eligible as a validator.
  * The top 50 validators by total stake are active.
* **Permissionless Non-Validating Nodes:** Testnet now supports running permissionless non-validating nodes.\
  Instructions: [GitHub – hyperliquid-dex/node](https://github.com/hyperliquid-dex/node)
* **Future Changes:**\
  Flags, ports, and other settings may change.
