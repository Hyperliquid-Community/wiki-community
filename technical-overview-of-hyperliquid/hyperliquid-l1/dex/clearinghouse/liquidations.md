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

Liquidation is a critical process on Hyperliquid L1 to ensure that traders maintain sufficient collateral and the platform remains solvent. It occurs when a trader’s account equity falls below the **maintenance margin** required for their positions. The platform uses multiple mechanisms to manage and resolve liquidations effectively, ensuring fairness and stability.

***

### **Overview of Liquidations** ⚠️

* **Maintenance Margin:**
  * Set at **half of the initial margin at max leverage**.
  * Varies depending on the asset’s maximum leverage (e.g., **1% for 50x leverage** or **16.7% for 3x leverage**).
* **Trigger:**
  * Liquidation is initiated when account equity (including unrealized PnL) drops below the maintenance margin.

***

### **Liquidation Process** 🔄

1. **📉 Partial or Full Close via Order Book:**
   * The Clearinghouse sends **market orders** to the book to close the position.
   * If the position is fully or partially closed to meet margin requirements:
     * **For Cross Margin:** Any remaining collateral is returned to the trader.
     * **For Isolated Margin:** Remaining collateral stays within the isolated position.
2. **🏦 Backstop Liquidation via Liquidator Vault:**
   * If the account equity drops below **two-thirds of the maintenance margin**, the **liquidator vault** steps in.
   * As part of the HLP strategy, the liquidator vault takes over the position and, on average, generates a profit.
   * Liquidator vault profits are redistributed to the community, unlike traditional venues where profits go to privileged market makers or the exchange operator.

***

### **Liquidation Price Calculation** 🧮

The liquidation price depends on leverage, position size, and margin available. For cross and isolated margin, the formula is:

```makefile
liq_price = price - side * margin_available / position_size / (1 - l * side)
```

Where:

* `price` = The **mark price**, which combines external CEX prices with Hyperliquid’s book state. This robust calculation ensures fairness, even during high volatility.
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

### **Key Takeaways** 📝

* Liquidations on Hyperliquid prioritize fairness and transparency, leveraging on-chain mechanisms like the **liquidator vault** to redistribute profits to the community.
* The **mark price**, derived from an advanced oracle system, ensures accurate and stable liquidation triggers, even during volatile conditions.
* **Auto-deleveraging** serves as the ultimate safeguard, protecting the platform from insolvency while maintaining fairness for all users.

By combining these mechanisms, Hyperliquid offers a robust and secure liquidation system that aligns trader incentives with the health of the ecosystem.
