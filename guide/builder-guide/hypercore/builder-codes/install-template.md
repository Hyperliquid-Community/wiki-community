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

# Install Template

To get started, you can either **clone the boilerplate repository** for a quick setup or **recreate it from scratch** to better understand its structure.

#### 🔗 **Template Repository**

You can find the template here: [GitHub - create-builder-codes-dapp](https://github.com/Solynor/create-builder-codes-dapp)

***

### **Option 1: Clone and Set Up the Repository**

#### **1️⃣ Clone the Repository**

Run the following command to clone the template:

```sh
git clone https://github.com/Solynor/create-builder-codes-dapp.git
cd create-builder-codes-dapp
```

Then install dependencies:

```sh
pnpm install  # or npm install
```

#### **2️⃣ Change the Git Remote to Your Own Repository**

To push your changes to a personal GitHub repository, update the remote URL:

```sh
git remote set-url origin git@github.com:your_name/repo_name.git
```

#### **3️⃣ Configure the Environment Variables**

Update the `.env` file with your custom settings - [RPC List](https://hyperliquid-co.gitbook.io/community-docs/guide/builder-guide/dapps-evm/evm-basics#id-1.-rpc-nodes-and-endpoints):

```ini
# The environment mode (development=testnet / production=mainnet) 
NEXT_PUBLIC_NODE_ENV=development

# The RPC URL for connecting to the HyperEVM  
NEXT_PUBLIC_RPC_URL=your_rpc_url  # [See RPC list on the doc]

# The builder's wallet address for fee collection  
NEXT_PUBLIC_BUILDER_ADDRESS=your_builder_address  # [Requires >100 USDC to enable the builder fee signer]

# The builder fee percentage (in basis points)  
NEXT_PUBLIC_BUILDER_FEE=10  # (0.1%)

# The WalletConnect project ID for wallet connections  
NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=your_wallet_connect_project_id  # [Create your project ID here: https://docs.reown.com/cloud/relay]
```

#### **4️⃣ Run the Application**

Once everything is set up, start the development server:

```sh
pnpm dev  # or npm run dev
```

Your application should now be up and running!

***

### Option 2: Build from Scratch

While cloning the boilerplate is faster, this approach helps you better understand the app’s architecture and dependencies.

***

### **1. Install Next.js**

We’ll start by setting up a new Next.js 15 project.

📌 **Run the following command:**

```sh
npx create-next-app@latest --use-pnpm
```

```
What is your project named? my-app
Would you like to use TypeScript? Yes
Would you like to use ESLint? Yes
Would you like to use Tailwind CSS? Yes
Would you like your code inside a `src/` directory? Yes
Would you like to use App Router? (recommended) Yes
Would you like to use Turbopack for `next dev`? Yes
Would you like to customize the import alias (`@/*` by default)? No
What import alias would you like configured? @/*
```

📚 **Reference**: [Next.js Installation Guide](https://nextjs.org/docs/app/getting-started/installation)

***

### **2. Project Structure**

Your app will be structured as follows:

#### 📁 **`app/`**

* **Houses Next.js routes and pages.**
* Main entry point for the application.

#### 📁 **`components/`**

* Stores **reusable components** for your pages.

#### 📁 **`hooks/`**

* Contains **custom React hooks** for logic reuse (e.g., `useAuth()`, `useFetchData()`).

#### 📁 **`lib/`**

* **`config/`** → Global settings (e.g., API URLs, environment variables).
* **`helpers/`** → Utility functions (e.g., `formatDate()`, `parseCookies()`).
* **`services/`** → API call logic (e.g., `authService.ts`, `userService.ts`).
* **`types/`** → TypeScript interfaces for better type safety.

***

### **3. Install & Configure Wagmi (Wallet Connection)**

Wagmi is used for **wallet connections** and blockchain interactions.

📌 **Install dependencies:**

```sh
pnpm add wagmi viem@2.x @tanstack/react-query
```

📚 **Reference**: [Wagmi Documentation](https://wagmi.sh/react/getting-started#manual-installation)

#### 🔧 **Modify the following files:**

**📁 `lib/config/`**

* **`index.ts`** → Fetches configuration from `.env`
*   **`wagmi.ts`** → Creates the Wagmi config using [AppKit Documentation](https://docs.reown.com/appkit/next/core/installation).

    ```sh
    pnpm add @reown/appkit @reown/appkit-adapter-wagmi
    ```
* **`chain.ts`** → Defines the Hyperliquid EVM testnet
*   **`axios.ts`** → Installs and configures Axios for API calls

    ```sh
    pnpm add axios
    ```

**📁 `components/`**

* **`ContextProvider.tsx`** → Wraps the app in `WagmiProvider` and passes the config.
* **`UserProvider.tsx`** → Manages user state based on wallet connection (`wagmi` + `localStorage`).
* **📌 Note:** Consider improving Builder Fee storage (DB or blockchain instead of local cache).

**📁 `lib/store.ts` (State Management)**

Zustand is used to **manage global state** efficiently.

📌 **Install Zustand:**

```sh
pnpm add zustand
```

**Responsibilities of `store.ts`:**

1. **Define user-related state types** (`User`, `Agent`, `UserStoreState`).
2. **Create Zustand store** for updating, resetting, and accessing user data globally.

📚 **Reference**: [Zustand Documentation](https://zustand.docs.pmnd.rs/getting-started/introduction)

***

### **4. UI & Styling Setup**

#### 📌 Install required packages:

```sh
pnpm add tailwindcss-animate class-variance-authority clsx tailwind-merge lucide-react
```

📚 **Reference**: [shadcn/UI Installation Guide](https://ui.shadcn.com/docs/installation/manual)

#### **Configure UI files**

* **`tailwind.config.ts`** → Customize Tailwind settings ([Example](https://github.com/sovrun-hl/create-builder-codes-dapp/blob/main/tailwind.config.ts))
* **`globals.css`** → Define base styles ([Example](https://github.com/sovrun-hl/create-builder-codes-dapp/blob/main/src/app/globals.css))
* **`lib/utils.ts`** → Utility functions for styling
* **`components/ui/`** → Copy & paste **shadcn/UI components** (e.g., `toast.tsx`, `button.tsx`, etc.).

📌 **Important:** shadcn/UI **is not a component library**—it's a collection of reusable UI components that you copy manually.

📚 **Reference:** [Radix UI (Shadcn's Base Library)](https://www.radix-ui.com/)

***

### **5. Blockchain Connection (Hyperliquid Integration)**

#### **Key Components:**

**📁 `app/page.tsx`**

* Displays **either the trading widget** (if connected) or the **wallet connection button**.

**📁 `components/`**

* **`ConnectWallet.tsx`** → Wraps a `Connect Wallet` button using AppKit.
* **`Trade.tsx`** → Trading widget for buying/selling assets.

**📁 `components/ApproveBuilderFee.tsx`**

* Ensures users approve the **Builder Fee** before trading.

**📁 `lib/services/`**

*   **`approve-builder.ts`** → Handles fee approval via Wagmi.

    🔹 **Setup Instructions:** Refer to the documentation [Dapp Setup Guide](../../hyperevm/evm-basics/dapp-setup.md#id-3.-dapp-less-than-greater-than-blockchain) for detailed steps on integrating your Dapp with the blockchain.

**📁 `lib/services/`**

* **`builder-info.ts`** → Calls Hyperliquid API `/info` endpoint ([API Docs](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint)).

***

### **6. Agent-Based Trading**

Hyperliquid allows **trading** via an "agent" account.

#### **Key Files:**

* **`components/ApproveAgent.tsx`**
  * Creates a new account (agent) for **secure order placement** without signing each time.
  * The agent **cannot move user funds**, making it a safer approach.
* **`lib/services/approve-agent.ts`**
  * Calls [Hyperliquid Exchange API](https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint) for agent approval.

📌 **Security Note:** The agent’s private key is generated **locally**—ensure it’s **never exposed or stored insecurely**.

***

### **7. Order Execution**

Handles placing, signing, and submitting trades.

#### **Key Services:**

* **`market-order.ts`** → `/exchange` (trade execution)
* **`mid-price.ts`** → `/info` (retrieves real-time mid-prices)
* **`balances.ts`** → `/info` (fetches user balances)
* **`token-details.ts`** → `/info` (retrieves token metadata)
*   **`signing.ts`** → Uses [MessagePack](https://msgpack.org/) for encoding.

    ```sh
    pnpm add @msgpack/msgpack
    ```

***

### **8. Final Steps: ESLint & Configuration**

📌 **Update ESLint rules (`eslint.config.mjs`):**

```js
jsCopierModifierrules: {
  "@typescript-eslint/no-unused-vars": "warn",
  "@typescript-eslint/ban-ts-comment": "warn",
}
```

📌 **Modify Next.js config (`next.config.ts`)**\
Check the [example file](https://github.com/sovrun-hl/create-builder-codes-dapp/blob/main/next.config.ts).

***

### **Conclusion**

By following this guide, you’ve built the **Builder Codes Dapp** from scratch, gaining a deep understanding of:&#x20;

✅ **Next.js & TypeScript setup**\
✅ **Wallet connection & Wagmi configuration**\
✅ **API integration with Hyperliquid**\
✅ **Trading execution with agent-based security**\
✅ **UI & state management with shadcn/UI & Zustand**
