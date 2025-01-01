---
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

# Margin Management

Margin management in Hyperliquid L1 ensures traders can efficiently use their capital while maintaining robust risk controls. Traders can choose between two margin modes—**Cross** and **Isolated**—depending on their risk appetite and trading strategy.

***

### **Margin Modes** ⚖️

#### **Cross Margin** 🌐

* **Shared Collateral:**\
  Positions in cross margin mode share a single collateral pool, maximizing capital efficiency.
* **Dynamic Margin Allocation:**\
  Unrealized profits (PnL) from winning trades are automatically added as margin for new or existing positions.
* **Risk Distribution:**\
  While efficient, losses on one position may impact the entire portfolio, as all positions draw from the same collateral.

#### **Isolated Margin** 🔒

* **Dedicated Collateral:**\
  Each position has its own dedicated collateral, isolating its risk from other trades.
* **Flexible Margin Adjustments:**\
  Traders can add or remove margin for individual positions after opening.
* **Granular Risk Management:**\
  Losses on one position do not affect others, providing better control over liquidation risks.

***

### **Initial Margin and Leverage** 🚀

#### **Leverage Options**

* Traders select leverage from **1x to a maximum that varies by asset** (ranging from \~3x to 50x).
* Higher leverage reduces the initial margin required but increases the risk of liquidation.

#### **Initial Margin Requirements**

* The formula for initial margin is:\
  **Initial Margin = (Position Size × Mark Price) ÷ Leverage**
* For **cross margin**, the initial margin is locked and cannot be withdrawn.
* For **isolated margin**, traders can adjust the margin after opening the position.

#### **Leverage Adjustments**

* Leverage is only checked when opening a position.
* After opening, traders must actively monitor risk. Actions to manage leverage include:
  * Partially or fully closing positions
  * Adding margin (isolated positions)
  * Depositing USDC (cross positions)

***

### **Maintenance Margin** 🛡️

#### **Definition:**

Maintenance margin ensures traders maintain enough collateral to avoid liquidation.

* At **max leverage**, maintenance margin is set to **half of the initial margin**.
  * Example: At 20x leverage, maintenance margin is **2.5% of the notional position**.

#### **Liquidation Triggers:**

* **Cross Margin:**\
  Liquidation occurs when the account equity (including unrealized PnL) falls below the required maintenance margin for all positions.
* **Isolated Margin:**\
  Liquidation is triggered independently for each position, based solely on its own margin and notional value.

***

Hyperliquid’s margining system is inspired by centralized exchanges, offering traders a familiar yet fully decentralized experience. Balancing efficiency and risk, it empowers users to optimize their trading strategies while safeguarding their capital.
