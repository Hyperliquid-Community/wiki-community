---
icon: crystal-ball
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

# Oracle

The **Hyperliquid Oracle System** plays a critical role in maintaining the accuracy and robustness of trading operations. It provides reliable price data for **funding rate calculations**, **margining**, **liquidations**, and the triggering of **Take Profit (TP)** and **Stop Loss (SL)** orders.

***

### **Spot Oracle Price** 📈

#### Definition:

The **spot oracle price** is computed by validators and serves as a critical input to both **funding rates** and the **mark price**.

#### Key Features:

* **Published by Validators Every 3 Seconds:** Ensures high-frequency updates for dynamic markets.
* **Weighted Median of CEX Prices:**
  * Prices are aggregated from major centralized exchanges (CEXs), including Binance, OKX, Bybit, Kraken, Kucoin, Gate IO, MEXC, and Hyperliquid itself.
  * **Weights:** Binance (3), OKX (2), Bybit (2), Kraken (1), Kucoin (1), Gate IO (1), MEXC (1), Hyperliquid (1).
  * **Final Price for Clearinghouse:**\
    The clearinghouse uses the **weighted median of validator-submitted prices**, with validators weighted by their **stake**.

### **Mark Price** 📊

**Definition:**

The mark price is an unbiased, robust estimate of the **fair price** for perpetual contracts.

#### **Components:**

* **Spot Oracle Price** combined with:
  * A **150-second EMA (Exponential Moving Average)** of the difference between Hyperliquid’s mid-price and the oracle price.
  * Median of the **best bid**, **best ask**, and **last trade** on Hyperliquid.
  * Median of Binance, OKX, and Bybit **perp mid-prices.**
* **Special Case:**
  * **If only two of the three inputs exist,** a **30-second EMA** of the median of best bid, best ask, and last trade on Hyperliquid is also included.
* **Usage:**
  * For **liquidations**, **margin calculations**, and **TP/SL** orders.
  * Computes **unrealized PnL** for active positions.
* **Update Frequency:** Updated approximately every **3 seconds**, in sync with oracle updates.

#### **Difference Between Spot Oracle Price and Mark Price** ⚖️

| **Spot Oracle Price**                                      | **Mark Price**                                          |
| ---------------------------------------------------------- | ------------------------------------------------------- |
| Published by validators every 3s.                          | Updated every 3s using spot oracle price.               |
| Weighted median of CEX spot prices and Hyperliquid prices. | Combines oracle prices and Hyperliquid order book data. |
| Used for funding rate calculations.                        | Used for liquidations, margining, and TP/SL triggers.   |

***

### **Uniswap Perpetuals** 🦄

Some perpetual contracts on Hyperliquid use **Uniswap V2 or V3 AMM prices** as their underlying spot asset.

* **Isolated-Only:**
  * These contracts do not allow cross margining or manual margin removal.
  * To adjust margin, positions must be partially or fully closed.
* **Conversion to USDT:**
  * Uniswap pool prices are converted to USDT using robust CEX oracle prices.

[Contract Addresses for Uniswap Pools](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/uniswap-perpetuals)

***

### **Margining and Oracle Usage** 💵

#### **USDC Margining with USDT Prices**

* **Primary Style:**
  * Oracle prices are denominated in **USDT**, while collateral is held in **USDC**.
  * This combination maximizes **liquidity** and **accessibility**.
* **Quanto Contracts:**
  * No conversion between USDC/USDT exchange rates occurs, meaning USDT P\&L is denominated directly in USDC.

#### **USDC-Denominated Contracts:**

* **Specific Assets:**
  * Only contracts with primary USDC liquidity (e.g., **PURR-USD** and **HYPE-USD**) have prices denominated in USDC.

***

This robust oracle system ensures Hyperliquid remains fair, reliable, and transparent for all traders.
