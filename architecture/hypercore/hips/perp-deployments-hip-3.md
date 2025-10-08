---
icon: chart-candlestick
---

# Perp Deployments (HIP-3)

### What is HIP-3 (Builder-Deployed Perpetuals)?

HIP-3 enables **permissionless deployment** of perpetual contract markets on Hyperliquid, marking a major step toward fully decentralizing the perp listing process. Any qualified user can manage their own perpetual DEX.

<figure><img src="../../../.gitbook/assets/HIP3_v2 (2).png" alt=""><figcaption></figcaption></figure>

#### How it works

* **Market deployment**
  * **Performant orderbooks** allocated directly on HyperCore
  * **Dutch auction** every 31 hours for deployment gas (paid in HYPE) - The first 3 assets per DEX are free
  * **Fully permissionless** process
* **Deployer responsibilities**
  * **Market definition**: oracle definition and contract specifications
  * **Market operation**: setting oracle prices, leverage limits and managing liquidity
  * Requires **third-party frontends** - not available on app.hyperliquid.xyz
* **Trading Experience**
  * **Fee:**
    * **2x usual base rate** (0.09%/0.03%) - **50% share** with the deployer
    * [User rebates](../dex/clearinghouse/fees-builder-codes.md) only affect the 50% of Hyperliquid fees
    * The net effect is that the protocol collects the same fee regardless of whether the trade is on an HIP-3 or a validator-operated perp
  * **Isolated margin only** initially (cross margin coming later)
  * **Quote Assets & Collateral**
    * Any [permissionless quote asset](https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/permissionless-spot-quote-assets) can be used as collateral
    * USDC/USDT eligible by default
    * Other stablecoins require **200k HYPE staked for 3 years**
    * **Aligned stablecoins** (additional requirements) offer fee reductions for traders

#### Requirements and security

* **Mandatory stake**
  * **500k HYPE minimum** stake required. Will decrease over time as the infrastructure matures
  * Stake locked for 30 days after all **perps halted**
  * **7-day unstaking queue** during which slashing can occur
* **Slashing mechanism**
  * **Purpose**: Prevent behavior jeopardizing protocol correctness, uptime, or performance
  * **Stake-weighted vote** by validators in case of malicious operation
    * **Invalid state transitions** or prolonged downtime: up to 100%
    * **Brief network issues**: up to 50%
    * **Performance degradation**: up to 20%
  * **Important Notes:** Slashed stake is **burned**, not redistributed

***

### Ecosystem impact

**New Markets**

* **Non-crypto perps**: traditional assets, commodities, indices
* **Niche markets**: specialized demand products
* **Financial innovation**: novel perpetual contract types

**Development Opportunities**

* **Specialized frontends** for HIP-3 markets
* **HYPE pooling protocols** for collaborative deployments
* **Multisig deployment** for shared market operation
* **Builder codes** for additional fee monetization

***

**Resources**: [Official Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-3-builder-deployed-perpetuals?q=stablecoin+issuer) | [API Documentation](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/hip-3-deployer-actions) | Companies working on HIP3 ([Dashboard](https://app.lit.trade/hip3) | [Chris Breakdown](https://x.com/chrisling_dev/status/1967614817436565946))

