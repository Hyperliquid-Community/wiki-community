---
icon: arrow-up-wide-short
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

# Order Book

The **Hyperliquid Order Book** is the backbone of trading on the platform, designed to function similarly to centralized exchanges but with the advantage of being fully **on-chain**. This ensures transparency and fairness while maintaining high-speed matching and robust operations.

***

### **Overview of the Order Book** 📘

* **Core Functionality:**\
  Each asset has its own order book, where orders are matched based on **price-time priority**.
* **Tick Size and Lot Size:**
  * Prices are placed as integer multiples of the **tick size**.
  * Sizes are specified as integer multiples of the **lot size**.
* **On-Chain Matching:**\
  All operations occur directly on-chain, integrating seamlessly with the **Clearinghouse** to ensure margin and position checks are consistently enforced.

#### **Key Features**:

1. **Fully On-Chain:**\
   Transparent and verifiable, with every operation recorded on the blockchain.
2. **Margin-Integrated:**\
   Margin checks are conducted when orders are placed and again when they match, ensuring resilience against oracle price fluctuations.
3. **Fair Matching:**\
   Orders follow a **price-time priority**, rewarding earlier placement at the same price level.

***

### **Order Types** 🛒

Hyperliquid offers a wide range of order types, catering to diverse trading strategies:

#### **Primary Order Types**:

* **Market Order:** Executes immediately at the current market price.
* **Limit Order:** Executes at the specified limit price or better.
* **Stop Market Order:** A market order activated when the price hits the stop price, used to **limit losses** or **lock in profits**.
* **Stop Limit Order:** A limit order triggered at a selected stop price.

#### **Advanced Order Types**:

* **TWAP (Time-Weighted Average Price):** Divides a large order into smaller sub-orders executed at intervals to minimize market impact.
  * **Details:** Sub-orders execute every **30 seconds**, targeting the TWAP schedule while limiting slippage to **3%**.
* **Scale Orders:** Places multiple limit orders within a defined price range to capture volatility effectively.

***

### **Order Options** ⚙️

* **Reduce Only:** Ensures the order only reduces an existing position rather than opening a new one in the opposite direction.
* **Good Til Cancel (GTC):** The order remains on the book until filled or canceled.
* **Post Only (ALO):** Adds an order to the book without executing it immediately.
* **Immediate or Cancel (IOC):** Cancels the order if it’s not immediately filled.
* **Take Profit (TP):** Triggers a market or limit order to close a position at a specific profit level.
* **Stop Loss (SL):** Triggers a market or limit order to close a position at a specified loss threshold.

#### **TP/SL Orders**:

* **Mark Price Triggered:** TP/SL orders are activated using the **mark price** for accurate execution.
* **Drag-and-Drop Editing:** Modify TP/SL directly on the TradingView chart.
* **Market vs. Limit TP/SL:**
  * **Market:** Executes with a 10% slippage tolerance.
  * **Limit:** Allows traders to control slippage with aggressive or conservative limit prices.

***

### **Contract Specifications** 📝

Hyperliquid’s perpetual contracts are designed for simplicity and efficiency, catering to both institutional and retail traders.

#### **Key Features**:

* **Linear Perpetuals:** Collateralized with **USDC**, but prices are denominated in **USDT** for liquidity and accessibility.
* **No Expiration:** Funding payments align perpetual prices with spot prices over time.
* **Position Limits:**
  * Maximum **market order values** range from **$250,000 to $4,000,000**, depending on leverage.
  * Maximum **limit order values** are **10x** the corresponding market order limit.

[Read more about Contract Specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications)

***

### **Index Perpetuals** 📊

In addition to spot-based perpetuals, Hyperliquid offers **index perpetual contracts**, which track formulas instead of spot prices.

* **Mechanism:** Validators periodically report the index formula’s value, which is used instead of a spot oracle price for funding calculations.
* **Example Applications:** Indices tracking market sentiment, weighted averages of token prices, etc.

[Learn more about Index Perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/index-perpetual-contracts)

***

### **Hyperps (Hyperliquid-Only Perps)** 🚀

A unique offering by Hyperliquid, **Hyperps** are perpetual contracts that don’t require an external spot or index oracle price.

* **Funding Rates:** Determined relative to an **8-hour exponential moving average** of the mark price, reducing susceptibility to manipulation.
* **Conversion to Vanilla Perps:** Once the underlying asset becomes widely traded on major platforms (e.g., Binance, Bybit), Hyperps transition to standard perpetual contracts.
* **Open Interest Caps:** Initially limited to **$1,000,000** for early market stability.

[Explore more about Hyperps](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/hyperps)

***

### **Perpetual Assets** 🌍

Hyperliquid supports trading for **100+ assets**, with new listings influenced by community input. Future plans include transitioning to a **decentralized and permissionless listing process**, ensuring broad accessibility.

***

The **Hyperliquid Order Book** combines the best features of centralized exchanges with the transparency and security of decentralized systems. By supporting diverse order types and contract styles, Hyperliquid ensures a robust and flexible trading experience for all users.
