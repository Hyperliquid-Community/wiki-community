---
icon: conveyor-belt-boxes
---

# API Servers

Hyperliquid utilizes API servers to provide fast, efficient access to blockchain data and trading functionalities. These servers act as **non-validating proxies**, forwarding user requests to the network’s validating nodes via **RPC calls**. This design ensures **scalability, flexibility, and efficient load balancing** for traders and developers.

### **How API Servers Work**

1. **User Request → API Server**: A user submits an API request (e.g., fetching market data, placing an order).
2. **API Server → Node RPC**: The API server **forwards** the request to a validating node using RPC.
3. **Node RPC → API Server**: The node **processes the request**, validates transactions, and includes them in a block if necessary.
4. **API Server → User**: The processed response is relayed back to the client.

#### **Key Benefits of API Servers**

* **Optimized Performance**: API servers maintain an **in-memory representation of blockchain state**, reducing query latency.
* **Scalability**: Multiple API servers can be deployed to **distribute traffic**, preventing bottlenecks.
* **DDoS Protection**: API servers act similarly to **sentry nodes**, preventing direct attacks on validators.
* **Familiar Interface**: API endpoints provide an experience similar to **centralized exchanges**, making it easier for algorithmic traders to interact with Hyperliquid.

### **Current State & Future Plans**

#### **🔹 Current Status: Not Yet Permissionless**

At present, API servers are **operated by Hyperliquid**, meaning users must rely on the official endpoints for requests. The permissionless model is not yet available.

#### **🔹 Future Vision: Fully Permissionless API Servers**

Hyperliquid plans to **decentralize API server deployment**, allowing anyone with access to an RPC node to spin up their own API server. This will enable:

* **Custom API deployments** with specific properties (e.g., private endpoints, custom rate limits).
* **More resilient infrastructure**, as multiple independent API servers reduce reliance on a single provider.
* **Greater decentralization**, ensuring that users are not dependent on a central API gateway.

### **REST vs WebSocket API**

Hyperliquid provides **two types of API connections**:

| Feature       | REST API                                 | WebSocket API                                  |
| ------------- | ---------------------------------------- | ---------------------------------------------- |
| **Usage**     | Request-response model                   | Real-time updates                              |
| **Data Flow** | Queries blockchain state on demand       | Pushes updates as new blocks are created       |
| **Speed**     | Slight delay due to consensus processing | Faster, updates are immediate                  |
| **Best for**  | Order execution, historical data         | Live market data, real-time trading strategies |

#### **Key Difference**

* **REST** interacts directly with **consensus nodes** and waits for **a transaction to be finalized in a committed block** before responding.
* **WebSocket** relies on a **parallel state replica** that updates clients **as blocks are produced**, but since it runs separately from consensus, **timestamps may slightly differ from REST responses**.

🔗 **For the documentation, visit:** [Hyperliquid API servers](https://hyperliquid.gitbook.io/hyperliquid-docs/hyperliquid-l1/api-servers)
