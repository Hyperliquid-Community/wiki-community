---
icon: recycle
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

# EVM Basics

This page covers the foundational EVM features you’ll need on Hyperliquid.

***

#### 1. RPC Nodes & Endpoints

Use any of the following endpoints to interact with the Hyperliquid **Testnet**:

* **Hyperliquid**: [https://rpc.hyperliquid-testnet.xyz/evm](https://rpc.hyperliquid-testnet.xyz/evm) (old one: api.hyperliquid-testnet.xyz/evm)
* **Luganodes**: [https://hyperliquid.lgns.xyz/](https://hyperliquid.lgns.xyz/)
* **ValiDAO**: [http://hyperliquid.testnet.rpc.validao.xyz/](http://hyperliquid.testnet.rpc.validao.xyz/)
* **Enigma**: [https://hyperliquid-rpc.enigma-validator.com/evm](https://hyperliquid-rpc.enigma-validator.com/evm)

> **Tip:** Choose the endpoint that best fits your region or latency needs. They all serve the same network.

***

#### 2. Block Explorers & Analysis Tools

Track transactions, verify contracts, and analyze on-chain activity with the following resources:

* **Tools Directory**: [Community & Projects Tools](https://hyperliquid-co.gitbook.io/community-docs/community-and-projects/ecosystem-projects/tools)
* Explorers often provide convenient API endpoints for fetching network data quickly.
  * [Hyperlend](https://explorer.hyperlend.finance/api-docs)
  * [Purrsec](https://testnet.purrsec.com/api/introduction)

***

#### 3. Main Contract Addresses (Testnet Only)

Here are some commonly used [**Testnet** contracts](https://explorer.hyperlend.finance/tokens?type=ERC-20) on HyperEVM:

* **mockBTC (MBTC)**: `0x453b63484b11bbF0b61fC7E854f8DAC7bdE7d458`
* **Purr**: `0xC003D79B8a489703b1753711E3ae9fFDFC8d1a82`
* **Hyperswap LP (HPSX)**: `0xddA44A39AaA3e2dcc8aFd78ca70b0718877188b5`
* **WETH**:
  * `0xADcb2f358Eae6492F61A5F87eb8893d09391d160`
  * `0xe0bdd7e8b7bf5b15dcDA6103FCbBA82a460ae2C7` Less common)&#x20;
* **Stacked USDe (sUSDe)**: `0x2222C34A8dd4Ea29743bf8eC4fF165E059839782`
* **USDC**:
  * `0x6fDbAF3102eFC67ceE53EeFA4197BE36c8E1A094`
  * (Less common) `0x24ac48bf01fd6CB1C3836D08b3EdC70a9C4380cA`
* **SolvBTC**: `0x4B85aCF84b2593D67f6593D18504dBb3A337D3D8`
* **Stacked Testh (stTESTH)**: `0xe2FbC9cB335A65201FcDE55323aE0F4E8A96A616`
* **HFUN**: `0x37adB2550b965851593832a6444763eeB3e1d1Ec`
* **CatBAL**: `0x26272928f2395452090143Cf347aa85f78cDa3E8`
* **Points**: `0xFe1E6dAC7601724768C5d84Eb8E1b2f6F1314BDe`
* **Jeff**: `0xbF7C8201519EC22512EB1405Db19C427DF64fC91`
* **Kei Stablecoin**: `0xE1A78f5B2FC080d7F34c47d703f19533097Ee34a`

> **HYPE**: As the native token of HyperEVM, HYPE does not have a deployed contract address. Its balance is fetched directly via RPC when connecting a wallet (similar to ETH on Ethereum). Use [`eth_getBalance` ](https://docs.blockscout.com/devs/apis/rpc/eth-rpc)to interact with it.

***

#### 4. dApp Setup & Deployment

To learn how to configure your application, integrate wallets (e.g., **Wagmi** or **WalletConnect**), and deploy contracts (using **Foundry**, **Hardhat**, or other tools), see the dedicated dApp Setup & Deployment page.

* **Next Steps:**
  * Set up your app (nextjs and wagmi) - [here](../api/builder-interface.md).
  * How to deploy a contract with wagmi or hardat.
  * How to interact with this contract on your dApp.
