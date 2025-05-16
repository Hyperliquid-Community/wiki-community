---
icon: cat
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

# Unit

Unit is an asset tokenization protocol seamlessly integrated with Hyperliquid. It creates bridges between major blockchains and Hyperliquid, enabling users to deposit and withdraw assets like **BTC, ETH, and SOL** directly to their Hyperliquid spot balance. Built exclusively for the Hyperliquid ecosystem by a team of experts from HRT, Jump, Fortress, and IDF cyber units, Unit enhances Hyperliquid's capabilities through:

* A **unified trading experience** for both spot and derivatives markets
* **Multiple capital onramps** from native chains to Hyperliquid
* **Portfolio margin** for improved capital efficiency
* **On-chain spot-futures basis trades** and options functionality
* **Verifiable treasury management** for protocols and DAOs

### How Unit Works

Unit operates through a decentralized **Guardian network** that bridges Hyperliquid with other blockchain networks:

* **Guardians** are off-chain servers that run special software called "agents" to monitor blockchains
* A **leader Guardian** organizes transactions while others verify them for accuracy
* Each Guardian watches for new events (like deposits) using an "indexer" system
* Guardians control wallets on both Hyperliquid and connected blockchains (like [Bitcoin](https://docs.hyperunit.xyz/developers/key-addresses/mainnet/bitcoin))
* **Important**: At least 2 out of 3 Guardians must agree before any funds move between chains

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p><a href="https://docs.hyperunit.xyz/architecture/quickstart">Architecture Overview</a></p></figcaption></figure>

Currently, three Guardians support the network: Unit, Hyperliquid, and Infinite Field. The off-chain nature of Guardians presents some centralization risks, but the system includes robust security measures:

* Multi-signature requirements protect against single points of failure
* Transactions are transparently recorded on both source and destination blockchains, making inconsistencies easily detectable
* Encrypted communications between Guardians prevent interception of sensitive data
* Secure storage of keys in specialized hardware environments (secure enclaves) defends against theft
* Transaction logging with digital signatures creates an immutable audit trail

Additionally, Unit implements comprehensive compliance protocols including OFAC sanctions screening and geoblocking where required by regulations.

The security and decentralization model will continue to improve as more Guardians join the network and the system becomes more permissionless.

#### Fee Structure

Unit charges fees on deposits and withdrawals to cover network costs and operational expenses. [Trading fees](https://x.com/hyperunit/status/1910728034656596205) remain the same as Hyperliquid's standard [fee](../hypercore/dex/clearinghouse/fees.md) structure. [Notably](https://x.com/cainosullivan/status/1891360551424721171), 100% of the seller fees assets (like BTC) are directed to the deployer address, providing a sustainable funding model for Unit's ongoing development and operation.

### Roadmap

* **First Integration** - Major crypto asset integration (BTC, ETH & SOL) ✅ completed on [May 15, 2025](https://x.com/hyperunit/status/1922801777407295658)
* Integration of various assets from Ethereum and Solana chains
* Addition of major blockchains to the network
* Network decentralization with a permissionless Guardian system

### Incidents

* [April 15, 2025](https://x.com/hyperunit/status/1912093926065856562): A Guardian went offline, causing latency in deposits and withdrawals.

### Resources

* All Unit functionality is integrated directly within Hyperliquid's interface
* Additional deposit and withdrawal options are available through:
  * [Unit's official website](https://app.hyperunit.xyz/)
  * [Developer API](https://docs.hyperunit.xyz/developers/api) for direct programmatic access
* [Hyperdash](https://unit.hyperdash.info/) provides a dashboard with statistics on deposits, withdrawals, and [more](https://x.com/hypurrdash/status/1890518525824901317)
* [Official documentation](https://docs.hyperunit.xyz/) contains comprehensive details, including [treasury addresses](https://docs.hyperunit.xyz/developers/key-addresses/mainnet)
