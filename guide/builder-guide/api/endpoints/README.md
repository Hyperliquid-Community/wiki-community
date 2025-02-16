---
icon: hand-point-right
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

# Endpoints

Hyperliquid provides both **REST** and **WebSocket** endpoints for accessing market data and executing trades. This page outlines the base URLs and the two API endpoints: `/info` and `/exchange`.

1. **Base URLs**
   * **HTTPS (REST API)**
     * **Mainnet:** `https://api.hyperliquid.xyz`
     * **Testnet:** `https://api.hyperliquid-testnet.xyz`
   * **WebSocket (WSS)**
     * **Mainnet:** `wss://api.hyperliquid.xyz/ws`
     * **Testnet:** `wss://api.hyperliquid-testnet.xyz/ws`
2. **API Endpoints Overview**
   * **`/info` Endpoint**\
     Provides various types of market and system information, classified into three categories:
     * [**General**](info/): General data.
     * [**Perpetuals**](info/perpetuals.md): Perpetual futures market data.
     * [**Spot**](info/spot.md): Spot market data.
   * **`/exchange` Endpoint**\
     Handles order execution and trading-related operations.

#### 📌 **Resources**

1. **Integration with CCXT (Less flexible):** [CCXT Docs](https://docs.ccxt.com/#/exchanges/hyperliquid)
2. **Testing Exchange Endpoint**
   * Use the Hyperliquid Python SDK: [Hyperliquid Python SDK](https://github.com/hyperliquid-dex/hyperliquid-python-sdk)
3. **Testing Info Endpoint in Postman:**

{% file src="../../../../.gitbook/assets/Solynor_hl-info.postman_collection (1).json" %}

***

#### 🔹 API Specificities

*   **Notation**

    The Hyperliquid v0 API uses a custom notation for some parameters. Key abbreviations:

    * **Px** → Price
    * **Sz** → Size (in base currency)
    * **Szi** → Signed size (+ for long, - for short)
    * **Ntl** → Notional value (USD amount, `Px * Sz`)
    * **Side** → Trade/book side (`B` = Bid/Buy, `A` = Ask/Sell)
    * **Tif** → Time in force (`GTC`, `ALO`, `IOC`)

    📌 **Full details:** [API Notation](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/notation)



*   **Tick & Lot Size**

    * Prices have a **maximum of 5 significant figures** but must respect decimal limits:
      * **Perps:** `MAX_DECIMALS = 6`
      * **Spot:** `MAX_DECIMALS = 8`
    * Sizes are rounded based on **szDecimals** for each asset.
    * To check `szDecimals`, query the **meta** request in the `/info` endpoint.

    📌 **Full details:** [Tick & Lot Size](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/tick-and-lot-size)



*   **Agent (API) Wallets & Nonce**

    * API wallets (agent wallets) can sign transactions on behalf of a master or sub-account. However:
      * API wallets **only sign transactions**; queries require the **actual account address**.
      * **Nonces are required** to prevent replay attacks.
      * Each API wallet tracks its own nonce state.
    * **Nonces & Transaction Ordering**
      * Hyperliquid L1 stores the **100 highest nonces per address**.
      * Each new transaction must have a **nonce greater than the smallest stored nonce** and must not be reused.
      * **Nonces expire after 1 day** from the L1 block timestamp.
    * **Best Practices for API Wallets**
      * Do **not reuse** API wallet addresses after deregistration. Generate a new wallet to avoid nonce pruning issues.
        * If using multiple subaccounts, assign **separate API wallets** to each one.
        * Market makers should **batch orders & cancels** every **0.1 seconds**, keeping **IOC/GTC orders separate from ALO orders** for prioritization.

    📌 **Full details:** [Agent Wallets & Nonces](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets)



*   #### **Error Responses**

    Errors are returned as a **vector** for batched requests or as a **single error** if the entire batch is invalid.

    * **Order Errors:** Tick size violation, insufficient margin, minimum order value ($10), reduce-only violations, invalid TP/SL price, no market liquidity.
    * **Cancel Errors:** Order not found (never placed, already canceled, or filled).
    * **Pre-validation Errors:** Affect entire batch (e.g., empty request, invalid tick size) and return a single response.

    📌 **More details:** [Error Responses](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/error-responses)



*   #### **Rate Limits**

    API usage is limited per **IP** and **L1 address**:

    * **REST API (Per IP):** 1200 requests/minute, request weight varies (1+ for batched orders, up to 40 for explorer API).
    * **WebSocket:** 100 connections, 1000 subscriptions, 2000 messages/min.
    * **L1 Address Limits:**
      * 1 request per 1 USDC traded since inception.
      * Initial buffer: 10,000 requests.
      * Cancels have a **higher limit** to ensure orders can still be canceled.
      * Batched requests count **once for IP limits** but **as n requests for L1 limits**.

    📌 **More details:** [Rate Limits](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/rate-limits)
