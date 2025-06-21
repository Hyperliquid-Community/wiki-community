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

* **Linear Perpetuals:** Collateralized with **USDC**, but prices are denominated in **USDT** for liquidity and accessibility (technically quanto contracts)
* **No Expiration:** Funding payments align perpetual prices with spot prices over time
* **Maximum market order values:** **$15M** (leverage ≥25), **$5M** (leverage 20-25), **$2M** (leverage 10-20), **$500K** (lower leverage)
* **Maximum limit order values:** **10x** the corresponding market order limit
* **Margin options:** Cross or isolated margin per wallet

_Note: PURR-USD and HYPE-USD are denominated in USDC due to their primary liquidity source being Hyperliquid spot._

[Read more about Contract Specifications](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications)

***

### **Index Perpetuals** 📊

In addition to spot-based perpetuals, Hyperliquid offers **index perpetual contracts**, which track formulas instead of spot prices.

* **Mechanism:** Validators periodically report the index formula's value, which is used instead of a spot oracle price for funding calculations
* **Current indices:** **NFTI-USD** (blue-chip NFT collections) and **FRIEND-USD** (friend.tech subjects)
* **Function:** Work exactly like normal perpetual contracts but track custom formulas rather than asset prices

[Learn more about Index Perpetuals](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/index-perpetual-contracts)

***

### **Hyperps (Hyperliquid-Only Perps)** 🚀

A unique offering by Hyperliquid, **Hyperps** are perpetual contracts that don't require an external spot or index oracle price.

* **Funding Rates:** Determined relative to an **8-hour exponential moving average** of the mark price, reducing susceptibility to manipulation
* **Conversion to Vanilla Perps:** Once the underlying asset becomes widely traded on major platforms (**Binance, OKX, Bybit**), Hyperps transition to standard perpetual contracts
* **Trading Restrictions:** **Low leverage** and **isolated margin only** - higher risk due to low liquidity, high volatility, and potentially extreme funding rates

⚠️ **Important:** Heavy price momentum creates strong funding incentives for opposite positions over the next 8 hours. Only trade contracts you fully understand.

[Explore more about Hyperps](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/hyperps)

***

### **Perpetual Assets** 🌍

Hyperliquid supports trading for **100+ assets**, with new listings influenced by community input. The protocol is transitioning to a **permissionless listing process** through [HIP-3](../hips/perp-deployments-hip-3.md) **(Builder-Deployed Perpetuals)**.

***

The **Hyperliquid Order Book** combines the best features of centralized exchanges with the transparency and security of decentralized systems. By supporting diverse order types and contract styles, Hyperliquid ensures a robust and flexible trading experience for all users.
