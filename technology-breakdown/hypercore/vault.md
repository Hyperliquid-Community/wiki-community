---
icon: chess-rook
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

# Vault

Vaults on **Hyperliquid L1** are powerful tools enabling both individual traders and the community to participate in advanced trading strategies. They **democratize access** to market-making profits and liquidation mechanisms, previously reserved for privileged parties on traditional exchanges.

***

## **Types of Vaults**

### **1. Protocol Vaults: Hyperliquidity Provider (HLP)** 🌐

#### **Overview**

The **Hyperliquidity Provider (HLP)** vault is a **community-owned** protocol vault that plays a vital role in the ecosystem:

#### **Key Roles**

* Engages in **multiple market-making strategies**
* Performs **liquidations** (via a dedicated liquidation strategy).
* Receives **a portion** of the **platform fees**.
* **Currently**, the HLP vault also receives **auction fees.**

#### **3-Core Strategies Used by HLP:**

* **Strategie A (**[0x010461c14e146ac35fe42271bdc1134ee31c703a](https://app.hyperliquid.xyz/vaults/0x010461c14e146ac35fe42271bdc1134ee31c703a)**):** A sophisticated market-making strategy that helps maintain liquidity without requiring you to create your own complex strategy or invest in separate funds.
* **Strategie B (**[0x31ca8395cf837de08b24da3f660e77761dfb974b](https://app.hyperliquid.xyz/vaults/0x31ca8395cf837de08b24da3f660e77761dfb974b)**):** Another advanced market-making approach working in tandem with Strategie A to optimize liquidity provision and risk management.
* **Liquidator (**[0x2e3d94f0562703b25c83308a05046ddaf9a8dd14](https://app.hyperliquid.xyz/vaults/0x2e3d94f0562703b25c83308a05046ddaf9a8dd14)**):** This component steps in during [backstop liquidations](https://community-hyperliquid.gitbook.io/community-docs/technical-overview-of-hyperliquid/hyperliquid-l1/dex/clearinghouse/liquidations), taking over positions from accounts that have fallen below their maintenance margin thresholds. It then exits these positions using a market-making algorithm, contributing to the platform’s stability.

#### **Community Participation**

* **Anyone can deposit liquidity** into the HLP vault to share in its profits.
* **No profit share fees** for vault owners—benefits are fully distributed to depositors.

#### **Lock-Up Period**

* Deposits have a **4-day lock-up period**.
* Withdrawals can only occur **4 days after the most recent deposit**.

***

### **2. Protocol Vaults: Assistance Fund (AF)** 🛡️

The **Assistance Fund (AF)** address ([0xfefefefefefefefefefefefefefefefefefefefe](https://hypurrscan.io/address/0xfefefefefefefefefefefefefefefefefefefefe)) is safeguarded by a **validator quorum**, ensuring that its usage is subject to strict conditions.

#### **Fee Allocation and Flow**

* Initially, it is **assumed** that trading fees from the Hyperliquid DEX were routed to the [0x36715f6408819492c27C1a1538156af9a2BFe963](https://hypurrscan.io/address/0x36715f6408819492c27C1a1538156af9a2BFe963) address, controlled exclusively by the Hyperliquid team, which then funded **0xfe**.
* However, there may have been **other addresses** involved in this process that are not publicly known.
* Currently, trading fees are sent **directly to 0xfe**, streamlining the process.

**On-Chain Visibility:**

* At present, **fees are not directly visible** on explorers, making it difficult to track fee flows or analyze their exact allocation.
*   _🚧 I will conduct a study to **estimate the fees generated** by the platform based on its trading volume._

    _Additionally, I will **review the Assistance Fund’s expenditures** to gain deeper insights into its activity._

**Automated Fund Activity:**

* Today, the Assistance Fund **constantly purchases HYPE tokens** using a **TWAP (Time-Weighted Average Price)** strategy. This ensures a steady and systematic buyback of HYPE using the trading fees it receives.

**Purpose**

* The Assistance Fund acts as a **safety net** during emergencies or special situations, providing stability and covering potential losses.

***

### **3. User Vaults** 👥

User-created vaults allow individuals to run personalized trading strategies and share profits with depositors.

#### **Vault Leaders:**

* **Profit Share:** Vault leaders receive **10% of the profits** generated by their strategies.
* **Requirements to Create a Vault:**
  * Deposit at least **100 USDC** to initialize.
  * Maintain at least **5% ownership** of the vault.
* Vault leaders execute trades directly from the Trade page, applying their strategy to the vault's balance.
* **Closing a Vault:**
  * Leaders must close all open positions before closing a vault.
  * Depositors receive their share of the vault’s assets upon closure.

#### **Vault Depositors:**

* **Earnings:** Depositors earn a share of the vault’s profits proportional to their contribution.
* **Lock-Up Period:** Deposits are locked for **1 day** before withdrawal is allowed.
* **Performance Tracking:**
  * View vault statistics, including APY, total deposits (TVL), and historical performance, on the vault’s page.
* **Withdrawals:**
  * If margin requirements are met, withdrawals do not affect open positions.
  * Otherwise, a proportional amount of positions is closed to maintain stability.

***

### **Risk Considerations** ⚠️

* Trading is inherently risky, and past performance does not guarantee future returns.
* Depositors should carefully review the performance history and strategy of a vault before committing funds.

***

### Resources 📚

For further reading and detailed insights on HLP, Assistance Fund, and Vaults, you can explore the following official resources:

* **HLP:** [Medium: HLP Overview](https://medium.com/@hyperliquid/hyperliquidity-provider-hlp-democratizing-market-making-bb114b1dff0f) | [Medium: 3-Month Update](https://medium.com/@hyperliquid/hlp-update-3-months-in-42327abe3e57)
* **AF:** [Docs: Trading Fees](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/fees)
* **Vaults:** [Docs: Vaults Overview](https://hyperliquid.gitbook.io/hyperliquid-docs/vaults) | [Vault Page](https://app.hyperliquid.xyz/vaults)
* **HL Revenue Analysis:** [Twitter Post](https://x.com/stevenyuntcap/status/1866326285703856272)

Vaults on Hyperliquid enable anyone—from DAOs to individual traders—to engage with sophisticated trading strategies, share in the ecosystem’s growth, and democratize access to advanced DeFi tools.
