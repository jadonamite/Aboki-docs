---

# **Component 3: Balance Management**

*How Aboki.xyz tracks, updates, and syncs user balances across Fiat + Crypto.*

---

## ** Purpose**

Balance Management handles all **real-time value tracking** for every user across **on-chain**, **off-chain**, and **fiat** layers.

It ensures that the app always knows:

* how much crypto a user owns
* how much fiat (NGN/USD) they have available
* what part of their balance is *locked* inside a P2P deal
* what part is available for **instant spend**

---

## ** Architecture Overview**

### **1. On-Chain Wallet Balance Layer**

Uses:

* Ethers.js / wagmi `useBalance`
* Fetches ERC-20 token balances (USDC, USDT, etc.)

**Purpose:**
Always reflect *true blockchain balances* inside the UI.

### **2. Off-Chain Internal Ledger**

You maintain a **database ledger** of user balances for:

* Fiat NGN
* Fiat USD
* Locked crypto inside P2P deals
* Pending settlements
* Historical balance changes

**Tables Needed:**

* `user_balances`
* `transactions`
* `locked_balances`
* `settlements`

This makes P2P swaps + escrow possible.

### **3. Balance Sync Engine**

A backend cron / listener that syncs:

* new on-chain transfers
* pending escrow releases
* completed swaps
* cash settlements

**Purpose:**
Keep the **front-end balance**, **ledger**, and **chain** consistent.

---

## **⚡ Key Features**

### **✔ Real-Time Crypto Balances**

Using wagmi + ethers to fetch:

* raw balance
* formatted balance
* block updates

### **✔ Fiat Balance Storage**

Stored entirely off-chain:

* `available_balance`
* `locked_balance`
* `pending_balance`

### **✔ Locked Balances for P2P Deals**

When a user creates or accepts a swap:

* Crypto becomes *temporarily locked* in your DB
* Fiat equivalent also gets locked
* Neither side can use that amount elsewhere

### **✔ Balance Events**

Every balance modification triggers:

* database insert
* event log
* UI refresh

Examples:

* swap initiated
* escrow funded
* swap completed
* funds released
* settlement triggered

---

## ** Front-End Hooks (React Example)**

```ts
// get crypto balance
const { data: cryptoBalance } = useBalance({
  address: user.walletAddress,
  token: USDC_ADDRESS,
});

// fetch fiat from backend
const { data: fiatBalance } = useQuery(["fiat-balance"], () =>
  api.get("/balance/fiat")
);
```

This gives you:

```
cryptoBalance: 23.5 USDC
fiatBalance: {
  ngnAvailable: 120000,
  ngnLocked: 45000,
  usdAvailable: 20,
  usdLocked: 5
}
```

---

## ** Output of This Component**

After implementing this component, Aboki.xyz has:

* live on-chain balances
* accurate fiat balances
* locked balances for P2P trades
* sync between chain ↔ backend ↔ UI
* stable P2P escrow flow

This is the core that makes the P2P system **safe**, **trustworthy**, and **smooth**.

---


```
[Next: Component 4 — Peer-to-Peer Transaction Engine](#component-4-peer-to-peer-transaction-engine)
```
