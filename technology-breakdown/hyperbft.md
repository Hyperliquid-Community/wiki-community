---
icon: handshake-simple
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

# HyperBFT

### What is Consensus in a Blockchain?

In a blockchain, the **consensus mechanism** ensures that all network participants agree on the state of the ledger—even if some actors are faulty or acting maliciously. It’s what maintains the trust and integrity of the system, enabling everyone to share a common view of which transactions are valid and included in the chain.

### About HyperBFT

Since we only know that HyperBFT is “heavily inspired” by Hotstuff **(no official HyperBFT docs yet)**, we can look at Hotstuff’s key features **to guess** what HyperBFT might offer:

#### **Key Points (Based on Hotstuff):**

* **🛡️ Byzantine Fault Tolerance (BFT) :** Hotstuff tolerates up to **1/3 malicious validators**, ensuring that even with some validators acting dishonestly, the network can still reach consensus.
* **⏱️ Pseudo-Synchrony:** Hotstuff operates asynchronously under normal conditions. In case of extended network issues, it shifts into a synchronous mode after a “Global Stabilization Time” (GST), guaranteeing that honest participants will eventually agree on a block.
* **👥 Shared State Across Separate Environments:** HyperBFT secures both the L1 and the HyperEVM by sharing the same state and data availability layers. Despite operating in distinct execution environments, this unified consensus ensures consistency and synchronization across the entire ecosystem, simplifying operations and maintaining a cohesive state. (Check out the [HyperEVM](hyperevm.md) page for more details!)
* **🔄 Rotating Leaders:** Hotstuff achieves consensus through rotating leaders over multiple rounds. In HyperBFT, we might see a similar pattern: each leader proposes a block, and if disagreement arises, the network moves to a new “view” or round with a different leader until consensus is found.

**Further Reading:** For a deeper dive into the fundamentals that inspired HyperBFT, you can read about Hotstuff here: [Understanding Hotstuff & Byzantine Fault Tolerance (Medium)](https://medium.com/@Elifhilalumucu/understanding-hotstuff-and-byzantine-fault-tolerance-393ca878173f).

_**Stay Tuned:** As soon as official HyperBFT documentation is released, we’ll update this section with precise details on how Hyperliquid’s custom consensus mechanism works._

### Performance Metrics

Understanding the performance of a blockchain’s consensus mechanism is critical for evaluating its scalability and usability.

* **Latency:** Median latency is **0.2 seconds**, while 99th percentile latency is **0.9 seconds**. This ensures transactions are processed rapidly under typical and peak traffic conditions.
* **Current Throughput:** While the L1 supports up to **200,000 orders per second**, its consensus and networking layers are designed to scale beyond **1 million orders per second** as execution logic is further optimized.

