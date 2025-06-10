---
icon: chart-candlestick
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

# Perp Deployments (HIP-3)

## HIP-3: Builder-Deployed Perpetuals

**Status:** Testnet only (MVP available)\
**Phase:** Testing and feedback collection - Specifications not finalized

### What is HIP-3?

**HIP-3** enables users to **permissionlessly deploy** their own perpetual contract markets on Hyperliquid. This feature represents a major milestone toward **fully decentralizing** the perp listing process.

Unlike centralized exchanges where only the team can list new markets, HIP-3 transforms any qualified user into a **"banker" of Hyperliquid**, capable of creating and managing their own perpetual markets.

#### How it works

* **Market deployment**
  * **Performant orderbooks** allocated directly on HyperCore
  * **Dutch auction** every 31 hours to pay deployment gas
  * **HYPE** used as gas token
  * **Fully permissionless** process
* **Deployer responsibilities**
  * **Market definition**: oracle definition and contract specifications
  * **Market operation**: setting oracle prices, leverage limits, settling if needed
  * **Fee sharing**: deployer receives up to 50% of Hyperliquid's base trading fees
  * **Fee configuration**: ability to add additional fees on top of base rate

#### Requirements and security

* **Mandatory stake**
  * **1M HYPE minimum** in permanent stake (can be pooled via multisig for collaborative deployment and operation)
  * Ensures market quality and protects users
  * Creates strong economic barrier against malicious actors
* **Slashing mechanism**
  * **Stake-weighted vote** by validators in case of malicious operation
  * **7-day unstaking queue** during which slashing can occur
  * Robust protection against harmful behavior

***

### Ecosystem impact

#### **New opportunities**

* **Non-crypto perps**: opening toward traditional assets
* **Specialized interfaces**: frontends dedicated to builder-deployed perps
* **HYPE pooling**: collaboration between projects to reach minimum stake

#### Important considerations

* **Market display**
  * [app.hyperliquid.xyz](https://app.hyperliquid.xyz/trade) will not initially display these perps
  * **No deployment UI** on official frontend
  * **Alternative interfaces** developed by the community (compatible with **builder codes** for additional fee monetization)
  * Encourages specialization and interface decentralization
* **Expected use cases**
  * **Legally sensitive assets** that the team cannot list directly
  * **Niche markets** with specific demand
  * **Financial innovation**: new types of perpetual contracts

***

### Resources

* **Official documentation:** [Hyperliquid Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals)
* **Feedback:** [Hyperliquid Discord](https://discord.com/invite/hyperliquid)
* **API documentation** and **Python SDK**: Coming soon

***

_HIP-3 marks Hyperliquid's evolution from a perp DEX to neutral, decentralized financial infrastructure, enabling anyone to become an institutional market maker._
