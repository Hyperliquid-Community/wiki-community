---
icon: coin-blank
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# Outcome Markets (HIP-4)

#### **What is HIP-4?**

HIP-4 brings **prediction markets** to Hyperliquid. You bet on a **Yes/No outcome** (e.g. "Will BTC be above $X tomorrow at 06:00 UTC?"), and each share pays **$1 if you're right, $0 if you're wrong**.

* **No leverage, no liquidations**: the most you can lose is what you paid
* **Price = probability**: a Yes share at $0.30 means the market sees a \~30% chance
* **First market**: a daily BTC binary, settled every day at **06:00 UTC** on the Hyperliquid BTC price

**How it works**

* **Two tokens per market**: **Yes** and **No**
  * At settlement, the winning side pays **1**, the losing side **0**
* **One shared order book**: buying Yes at $0.30 = selling No at $0.70, so all liquidity is pooled
* **Multi-choice markets** (e.g. "Who wins the election?"): several outcomes, **only one wins**

**Deployment**

* **Permissionless** since August 2026: anyone can launch outcome markets
* Requires a **500k HYPE stake**
* Markets must follow **templates approved by validators**

**Why it matters**

* **Same account for everything**: trade outcomes, spot and perps with the **same collateral**
* **Easy hedging**: e.g. long BTC perp + a binary on BTC as protection, all on Hyperliquid
* **New revenue for builders**: fees shared **50/50 between deployer and protocol**, plus **builder codes**

Resources: [Official Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-improvement-proposals-hips/hip-4-outcome-markets) | [Castle Labs](https://hyperliquidresearch.xyz/research/hip-4-making-all-markets-hyperliquid) | [Four Pillars](https://hyperliquidresearch.xyz/research/permissionless-deployment-triples-hip-4-volume-with-permission-the-remaining-constraint)
