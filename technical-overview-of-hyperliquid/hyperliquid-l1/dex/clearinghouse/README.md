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

# Clearinghouse

The **Clearinghouse** is the backbone of trading on Hyperliquid L1. It manages all user balances, open positions, and risk parameters to ensure seamless and fair trading. Every aspect of perpetual and spot trading, from deposits to liquidations, runs through this core component.

### **Key Responsibilities** 🛠️

* **📊 Balance & Position Management:**\
  Tracks user deposits, withdrawals, and margin balances while managing all open positions. This includes both perpetual and spot trading states.
* **⚖️ Margin Modes (Cross & Isolated):**\
  Supports flexible margin setups—cross margin for shared collateral across positions and isolated margin for independent risk management on specific positions.
* **📉 Leverage & Maintenance Margin:**\
  Ensures traders stay within their selected leverage limits and maintains system stability by enforcing initial and maintenance margin requirements.
* **🚨 Liquidations:**\
  Monitors account equity to prevent insolvency. When equity drops below maintenance requirements, the Clearinghouse handles liquidation processes through the order book or liquidator vault.
* **📈 Funding Rates:**\
  Calculates periodic funding rates to align perpetual contract prices with the underlying asset, ensuring market fairness.
* **📡 Oracle Integration:**\
  The Clearinghouse relies on an **oracle system** for price accuracy. The final price used is a **weighted median** of validator-submitted oracle prices, ensuring transparency and reliability. Validators' weights are based on their stakes.
