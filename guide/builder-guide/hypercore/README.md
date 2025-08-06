---
icon: arrows-to-circle
---

# HyperCore

The **Hyperliquid API** lets users and builders interact directly with the network, enabling seamless automation, integration, and innovation. Whether you're optimizing trading strategies or creating new financial products, the API provides the flexibility to build and earn rewards through on-chain activity.

1. **Automate and Optimize Trading**
   * Implement **trading bots** to execute market-making, delta-neutral, or other algorithmic strategies.
   * Manage orders programmatically with minimal latency and direct access to Hyperliquid’s liquidity.
2. **Incorporate Builder Codes -** [**Learn More**](../../../architecture/hypercore/dex/clearinghouse/fees-builder-codes.md#builder-codes)
   * **Builder codes** allow builders to set an additional fee, on top of Hyperliquid’s fees, of up to **0.1% for perpetuals** and **1% for spot**.
   * The user must sign to approve these fees, and for each trade made through this interface, they will pay **Hyperliquid fees + the builder fee**.

#### Resources

* 📚 [Endpoint Explanation](endpoints/) → Detailed breakdown of all API endpoints and the [Official Hyperliquid API Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api).
* 🛠️ [Builder Codes Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/trading/builder-codes) → How to implement builder codes.
* 🎥 [Jeff’s Video on Builder Codes](https://www.youtube.com/watch?v=WeRh589I76o\&ab_channel=WhenShiftHappens) → Overview of Hyperliquid’s vision and builder incentives.
* 💧 [Testnet Faucet](https://hyperliquid.gitbook.io/hyperliquid-docs/onboarding/testnet-faucet) → Get test tokens for the Hyperliquid testnet.

{% hint style="success" %}
**Stay Updated:** Check pinned messages in the <kbd>#api-announcements</kbd> Discord channel for the latest updates. If you have **questions**, head over to <kbd>#api-traders</kbd>, that’s the best place to ask!
{% endhint %}
