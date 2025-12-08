Here is **Component 5**, clean, structured, and matching the exact style of previous components.

---

# **Component 5: Hybrid Settlement — Crypto → Bank**

_Bridging on-chain crypto with off-chain banking to enable instant NGN/fiat payouts._

---

## **🎯 Purpose**

Component 5 powers **withdrawals**, **liquidity circulation**, and **real-world payouts**.

It connects:

- crypto balances
- fiat balances
- bank accounts
- settlement rails (Paystack, Monnify, Sterling, Interswitch, etc.)

This is what allows Aboki users to:

- withdraw NGN to any bank
- receive payouts after trades
- convert crypto → cash seamlessly

---

## **🏗️ Architecture Overview**

### **1. Two-Balance Model (Crypto & Fiat)**

Every user maintains:

| Balance Type       | Used For                                             |
| ------------------ | ---------------------------------------------------- |
| **Crypto Balance** | On-chain USDC/USDT/SOL or internal ledger equivalent |
| **Fiat Balance**   | NGN used for P2P and withdrawals                     |

Hybrid settlement requires **moving value across these two worlds safely**.

---

### **2. Fiat Liquidity Pool (Admin/Automated)**

For fiat withdrawals, the system needs liquidity.

Options:

- Admin-controlled bank account
- Automated Paystack/Monnify merchant wallet
- Dedicated settlement bank account

Withdrawals are processed from this pool.

---

### **3. Crypto → Fiat Conversion Logic**

Conversion uses:

- live price feed
- stablecoin swaps
- internal pricing engine

Example:
User wants to withdraw **20,000 NGN**:

1. Determine rate (e.g., 1 USDT = ₦1600)
2. Deduct equivalent crypto from user
3. Add NGN to user’s fiat balance
4. Process NGN payout to their bank

---

### **4. NGN Withdrawal Workflow**

#### **Step 1 — User Initiates Withdrawal**

Inputs:

- bank name
- account number
- amount
- pin

System verifies:

- enough fiat balance
- user KYC
- withdrawal limits
- device fingerprint

---

#### **Step 2 — Create Withdrawal Record**

Database entry:

```
id
user_id
amount
bank
account
status: pending|processing|completed|failed
provider: paystack|monnify
```

---

#### **Step 3 — Send Out Payment**

Via provider API:

- initiate payout
- receive reference
- mark as `processing`

---

#### **Step 4 — Webhook Confirmation**

Provider responds:

- successful
- failed

System updates:

- on success → **deduct fiat balance**
- on failure → **refund fiat balance**

---

### **5. Settlement Reconciliation**

Automated daily job:

- verify all payouts match DB
- sync balances
- log mismatches
- alert admin

---

### **6. Waterfall Fallback (Optional)**

If Provider A is down:

- reroute to Provider B
- or use Admin fallback payout

This ensures **high availability**.

---

## **⚡ Key Features**

### ✔ Instant NGN bank transfers

Fast settlement via API providers.

### ✔ Automatic reconciliation

No mismatched balances.

### ✔ Hybrid crypto–fiat conversion

Uses stablecoins + price engine.

### ✔ Secure payout approval

PIN + fingerprint + device security.

### ✔ High-availability fallback

If Paystack fails → Monnify → Manual.

---

## **📡 Backend Flow Example**

```
User requests withdrawal
↓
Check fiat balance, KYC, limits
↓
Create withdrawal record
↓
Call provider API
↓
Provider webhook → success
↓
Update record to COMPLETED
↓
Deduct fiat balance
↓
Notify user
```

---

## **🧩 Output of This Component**

After Component 5, Aboki gains:

- real NGN payouts
- crypto → cash conversion
- settlement automation
- reconciliation pipeline
- reliable payout flow

This makes Aboki a functioning **hybrid financial platform**, bridging both worlds.

```
[Next: Component 6 — Merchant Payment System](#component-6-merchant-payment-system)
```
