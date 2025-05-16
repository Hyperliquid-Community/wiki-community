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

# Template Update

Now that you have the **Builder Codes Dapp** set up, this guide will walk you through modifying and expanding its functionality.&#x20;

***

### **Customizing the Connect Wallet Modal (Reown AppKit)**

The default wallet connection modal is powered by **Reown AppKit**, which can be **themed, customized, and extended** with additional functionalities.

#### **1. Modify the Theme & Modal Options**

You can change the modal’s **appearance and behavior** by updating the configuration inside `createAppKit()`.

📌 **Reference:** [Reown AppKit Theming Docs](https://docs.reown.com/appkit/vue/core/theming#themevariables)\
📌 **More Modal Options:** [Reown AppKit Options](https://docs.reown.com/appkit/next/core/options)

```ts
// Create the modal with custom settings
export const modal = createAppKit({
  adapters: [wagmiAdapter],  
  projectId, 
  networks: [hypeEvmTestnet, arbitrumSepolia],  // Supported networks
  defaultNetwork: hypeEvmTestnet,  // Default blockchain network
  metadata: metadata,
  features: {
    analytics: true,  // Optional analytics tracking (defaults to Cloud settings)
  },
  themeVariables: {
    "--w3m-accent": "#262626"
    "--w3m-font-size-master": "9px",
  },
});
```

#### **2. Customizing the Connect Button**

To use the **default** Connect Wallet button, simply add this in your UI:

```tsx
{/* @ts-ignore */}
<appkit-button />
```

📌 **Customizing the button:** You can pass additional props to modify its behavior.\
📚 **Reference:** [AppKit Button Docs](https://docs.reown.com/appkit/next/core/components)

***

## **Updating API Calls: Using TypeScript Enums and Services**

To ensure **type safety**, **better organization**, and **easier maintenance**, we will follow a structure similar to the **Hyperliquid TypeScript SDK** when handling API requests.

***

### **1. Define Constants for API Calls**

To make API calls more structured, we define **enums** for the available request types.

📁 **`lib/types/constants.ts`**

```ts
// Enums for API info calls
export enum InfoType {
    ALL_MIDS = "allMids",
    META = "meta",
    OPEN_ORDERS = "openOrders",
    FRONTEND_OPEN_ORDERS = "frontendOpenOrders",
    USER_FILLS = "userFills",
    USER_FILLS_BY_TIME = "userFillsByTime",
    USER_RATE_LIMIT = "userRateLimit",
    ORDER_STATUS = "orderStatus",
    L2_BOOK = "l2Book",
    CANDLE_SNAPSHOT = "candleSnapshot",
    PERPS_META_AND_ASSET_CTXS = "metaAndAssetCtxs",
    PERPS_CLEARINGHOUSE_STATE = "clearinghouseState",
    USER_FUNDING = "userFunding",
    USER_NON_FUNDING_LEDGER_UPDATES = "userNonFundingLedgerUpdates",
    FUNDING_HISTORY = "fundingHistory",
    SPOT_META = "spotMeta",
    SPOT_CLEARINGHOUSE_STATE = "spotClearinghouseState",
    SPOT_META_AND_ASSET_CTXS = "spotMetaAndAssetCtxs",
    PREDICTED_FUNDINGS = "predictedFundings",
    SPOT_DEPLOY_STATE = "spotDeployState",
    TOKEN_DETAILS = "tokenDetails",
    MAX_BUILDER_FEE = "maxBuilderFee",
    HISTORICAL_ORDERS = "historicalOrders",
    USER_TWAP_SLICE_FILLS = "userTwapSliceFills",
    SUB_ACCOUNTS = "subAccounts",
    VAULT_DETAILS = "vaultDetails",
    USER_VAULT_EQUITIES = "userVaultEquities",
    USER_ROLE = "userRole",
    DELEGATIONS = "delegations",
    DELEGATOR_SUMMARY = "delegatorSummary",
    PERPS_AT_OPEN_INTEREST_CAP = "perpsAtOpenInterestCap",
    DELEGATOR_HISTORY = "delegatorHistory",
    DELEGATOR_REWARDS = "delegatorRewards",
}
```

📁 **`lib/types/constants.ts`** (Exchange API Enums)

```ts
export enum ExchangeType {
    ORDER = "order",
    CANCEL = "cancel",
    CANCEL_BY_CLOID = "cancelByCloid",
    SCHEDULE_CANCEL = "scheduleCancel",
    MODIFY = "modify",
    BATCH_MODIFY = "batchModify",
    UPDATE_LEVERAGE = "updateLeverage",
    UPDATE_ISOLATED_MARGIN = "updateIsolatedMargin",
    USD_SEND = "usdSend",
    SPOT_SEND = "spotSend",
    WITHDRAW = "withdraw3",
    SPOT_USER = "spotUser",
    VAULT_TRANSFER = "vaultTransfer",
    SET_REFERRER = "setReferrer",
    USD_CLASS_TRANSFER = "usdClassTransfer",
    TWAP_ORDER = "twapOrder",
    TWAP_CANCEL = "twapCancel",
    APPROVE_AGENT = "approveAgent",
    APPROVE_BUILDER_FEE = "approveBuilderFee",
}
```

***

### **2. Create API Service Files**

Now, we’ll structure API calls in `lib/services/` and use our enums to ensure better **type safety**.

#### 📁 **`lib/services/info/spot.ts`**

Handles Spot Market data requests.

```ts
tsCopierModifierimport axios from "@/lib/config/axios";
import { InfoType } from "@/lib/types/constants";
import { SpotClearinghouseStateResponse } from "@/lib/types/dashboard";

/**
 * Fetches the Spot Clearinghouse State for a given user.
 * @param user - The user's unique identifier.
 * @returns A promise resolving to the spot clearinghouse state data.
 */
export async function getSpotClearinghouseState(user: string) {
    try {
        const response = await axios.post(`/info`, {
            type: InfoType.SPOT_CLEARINGHOUSE_STATE, // Using Enum for safety
            user,
        });

        if (!response.data) {
            throw new Error("No data received from server");
        }

        return response.data as SpotClearinghouseStateResponse;
    } catch (error) {
        return Promise.reject(error);
    }
}
```

Do the same for:\
📁 **`lib/services/info/perp.ts`**\
📁 **`lib/services/info/general.ts`**\
📁 **`lib/services/exchange.ts`**

***

### **3. Using API Calls in Your Application**

Instead of manually calling `axios.post()`, you can now simply use the helper functions we defined.

Example usage in a **React component with `useQuery`**:

```ts
tsCopierModifierimport { useQuery } from "@tanstack/react-query";
import { getSpotClearinghouseState } from "@/lib/services/info/spot";

const { data: spotBalanceData, isLoading: isLoadingBalances, error: balanceError } = useQuery({
    queryKey: ["balances", address],
    queryFn: () => (address ? getSpotClearinghouseState(address) : null),
    enabled: !!address, // Only run if an address is available
});
```
