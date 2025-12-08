Here is **Component 6** — clean, structured, and in the same format as all previous components.

---

# **Component 6: Merchant Payment System**

*Enabling businesses to accept crypto + fiat payments seamlessly.*

---

## **🎯 Purpose**

Component 6 allows **merchants, vendors, online stores, and service providers** to accept payments through Aboki.

This creates an ecosystem where:

* users can pay merchants in USDC/USDT or NGN
* merchants instantly receive stable value
* settlement can happen in **crypto or NGN**

This turns Aboki into a **payment network**, not just a P2P app.

---

## **🏗️ Architecture Overview**

### **Merchant Accounts**

A merchant has:

* **Merchant Profile**
* **Merchant Wallet (smart contract account)**
* **Merchant Dashboard**
* **Merchant API Keys** (for online integrations)

Merchants operate differently from normal users:

* Higher limits
* Business-level KYC
* Settlement preferences
* Transaction analytics

---

## **📦 Core Features**

### **1. Merchant QR Payment**

Every merchant gets a unique QR code containing:

```
merchant_id  
merchant_wallet  
store_name  
payment_mode  
```

Users simply scan → amount → confirm → merchant gets paid instantly.

Supports:

* **NGN payments**
* **USDC payments**
* **Hybrid (pay in crypto, merchant receives NGN)**

---

### **2. Merchant Checkout API (Online Payments)**

Merchants can integrate Aboki using something like:

```
POST /v2/payments/checkout
{
  amount: 20000,
  currency: "NGN",
  merchant_id: "...",
  description: "Order #392"
}
```

Reply contains:

* checkout URL
* payment QR
* deep link

Users pay inside Aboki → instantly settle.

---

### **3. Settlement Options**

Merchants choose **settlement preference**:

### 🔹 **Option A — Receive Crypto (USDC/USDT)**

Faster, purely on-chain.

### 🔹 **Option B — Receive NGN (Fiat Payout)**

Uses Component 5 hybrid settlement.
Funds move to merchant’s fiat balance and can be withdrawn to bank.

### 🔹 **Option C — Auto-Convert (Crypto → NGN)**

Smart conversion with internal price engine.

---

### **4. Merchant Dashboard Features**

Merchants can view:

* total sales
* transactions
* settlement history
* fiat balance
* crypto balance
* export CSV

Also supports:

* refund requests
* dispute resolution
* admin override features

---

### **5. Merchant Transaction Flow**

```
User scans merchant QR
↓
User enters amount
↓
User confirms payment (biometric + passkey)
↓
Crypto transfer to merchant wallet (or internal ledger)
↓
If NGN settlement:
  auto-convert + credit merchant fiat balance
↓
Notify merchant:
  "Payment received"
```

This flow uses:

* Coinbase Smart Wallet
* Gasless transactions
* On-chain or off-chain hybrid logic

---

## **⚙️ Technical Implementation**

### Smart Contract Layer

Each merchant uses:

* **Smart Wallet Account**
* contract modules enabling:

  * payment hooks
  * callback triggers
  * logging

### Backend Layer

Endpoints required:

```
POST /merchant/create
POST /merchant/login
GET  /merchant/stats
POST /merchant/withdraw
POST /merchant/payment/init
POST /merchant/payment/verify
```

### Frontend Layer

Build pages:

* Merchant registration
* Payment scanner
* Sales dashboard
* Settlement screen

---

## **📌 Why This Matters**

This component transforms Aboki from a **trading app** into a **payments infrastructure**, enabling:

* offline merchant acceptance
* online checkout
* crypto payment rails
* instant payouts
* business onboarding

When this is live → you have **MTN MoMo + Paystack + P2P crypto** all in one system.

---

```
[Next: Component 7 — Gasless Infrastructure (The Paymaster)](#component-7-gasless-infrastructure-the-paymaster)
```
