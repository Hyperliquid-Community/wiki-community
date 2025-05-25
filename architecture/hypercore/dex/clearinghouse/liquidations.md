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

# Liquidations

Liquidation is a critical process on HyperCore to ensure traders maintain sufficient collateral and the platform remains solvent. It occurs when a trader's account equity falls below the **maintenance margin** required for their positions.

***

### **Overview of Liquidations** ⚠️

* **Maintenance Margin:** Set at **half of the initial margin at max leverage** - varies from **1.25% (40x leverage)** to **16.7% (3x leverage)** depending on the asset
* **Trigger:** Liquidation initiates when account equity drops below maintenance margin
* **Mark Price Based:** Uses [mark price](../oracle.md#mark-price) (combining external CEX prices with Hyperliquid's book state) rather than instantaneous book price for robust liquidation triggers

***

### **Liquidation Process** 🔄

1. **Market Order Liquidation**
   * The Clearinghouse sends **market orders** to the book to close the position.
   * **Large positions (>$100K USDC):** Only **20% liquidated** initially to avoid overwhelming the order book
   * **30-second cooldown** after partial liquidation - if the position is still liquidable after the cooldown, subsequent market orders target the entire remaining position
   * All users can compete for liquidation flow - **no clearance fees**
   * Any remaining collateral is returned to the trader if position successfully closes
2. **Backstop Liquidation (Liquidator Vault):**
   * Triggers when account equity drops below **2/3 of maintenance margin**
   * **Liquidator vault** (part of HLP strategy) takes over the position and, on average, generates a profit.
   * **Cross positions:** All cross positions and margin transferred to liquidator
   * **Isolated positions:** Only that specific position and margin transferred
   * **Community profits:** Liquidation profits go to HLP holders, not privileged market makers

***

### **Liquidation Price Calculation** 🧮

```lua
liq_price = price - side * margin_available / position_size / (1 - l * side)
```

Where:

* `price` = mark price
* `l = 1 / MAINTENANCE_LEVERAGE`
* `side = 1` for long positions, `-1` for short positions
* `margin_available (cross) = account_value - maintenance_margin_required`
* `margin_available (isolated) = isolated_margin - maintenance_margin_required`

***

### **Auto-Deleveraging** 🔐

When all other liquidation mechanisms are insufficient to resolve a trader’s negative balance, **auto-deleveraging (ADL)** is triggered to ensure the platform’s solvency:

1. **Triggered Condition:**
   * A trader’s account value or isolated position value becomes negative, creating potential bad debt.
2. **Process:**
   * Traders on the opposite side of the position are ranked by **unrealized PnL** and **leverage used**.
   * Positions are closed at the previous **oracle price** against the underwater trader.
   * This ensures no bad debt is created, and the platform remains solvent.
3. **Platform Guarantee:**
   * Users with no open positions are never forced to socialize any platform losses.

***

### **Key Benefits** ✅

* **Transparent system:** No hidden fees, community gets liquidation profits via HLP
* **Capital preservation:** Traders keep remaining margin when successfully liquidated via order book
* **Democratic access:** All users can participate in liquidation flow, not just privileged market makers
* **Robust pricing:** Mark price system prevents manipulation during volatile periods
* **Auto-deleveraging** serves as the ultimate safeguard, protecting the platform from insolvency while maintaining fairness for all users.

The liquidation system prioritizes fairness, transparency, and capital preservation while maintaining platform solvency through multiple protective layers.
