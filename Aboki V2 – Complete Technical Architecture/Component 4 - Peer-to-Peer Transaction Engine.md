# **Component 4: Peer-to-Peer Transaction Engine**

_The core logic that powers matching, escrow, swaps, negotiation, and settlement across users._

---

## ** Purpose**

This is **the heart of Aboki.xyz**.

The P2P Engine handles:

- creating swap offers
- matching users
- locking crypto/fiat
- managing escrow
- confirming payments
- releasing funds
- resolving disputes

Everything that makes Aboki function as a **marketplace + exchange + escrow system** lives here.

---

## ** Architecture Overview**

### **1. Offer Creation**

Users can:

- create buy offers
- create sell offers
- set rates
- set limits
- choose tokens (USDC, USDT, etc.)
- choose fiat (USD, NGN)

Stored in DB:

`offers` table fields:

- user_id
- token
- type (buy/sell)
- amount
- min/max
- rate
- status

---

### **2. Matching Engine**

Matches two users when:

- seller has enough crypto
- buyer has enough fiat
- rate conditions satisfy
- neither user has an active locked trade

If matched → creates a `deal`.

---

### **3. Deal / Escrow Lifecycle**

#### **Deal Creation → Pending**

A `deal` entry is created in DB:

- deal_id
- buyer_id
- seller_id
- crypto_amount
- fiat_amount
- rate
- timestamps

Crypto equivalent is **locked** from the seller’s available balance.
Fiat equivalent is **locked** from the buyer’s balance.

#### **Seller Sends Crypto (If On-Chain Escrow)**

If using a smart-contract escrow:

- seller signs transaction
- contract holds funds

If using internal ledger (off-chain escrow):

- balance is moved from `available` → `locked`

#### **Buyer Sends Fiat**

Buyer uploads proof or initiates direct payment.

#### **Confirmation Stage**

Two confirmations must happen:

- **Buyer confirms** “fiat sent”
- **Seller confirms** “fiat received”

Both → triggers settlement.

#### **Settlement Stage**

System releases:

- crypto to buyer
- fiat to seller

Database updates:

```
locked → available
locked → available (other side)
```

---

### **4. Dispute System**

If a user reports a dispute:

- deal enters `REVIEW`
- both parties submit evidence
- admin resolves
- release funds to correct party

---

### **5. Transaction Finalization**

After completion:

- deal archived
- balances updated
- transaction log generated
- notifications pushed

---

## **⚡ Key Features**

### ✔ **Offer Book (Buy/Sell)**

Like a mini order book.

### ✔ **Escrow Logic**

Crypto + fiat both locked before swap.

### ✔ **Price Engine**

Reads:

- market price (CoinGecko or oracle)
- user’s rate
- premium/discount

### ✔ **Time-outs**

If one user delays beyond N minutes:

- auto-cancel
- auto-unlock balances

### ✔ **Notifications**

Push when:

- matched
- payment sent
- payment received
- dispute opened
- completed

---

## **📡 Backend Flow Example**

```
User A creates offer
↓
User B matches offer
↓
Create deal entry
↓
Lock crypto + fiat balances
↓
Buyer sends fiat → clicks "I sent"
↓
Seller confirms "I received"
↓
Release funds
↓
Update balances
↓
Mark deal COMPLETED
```

---

## **🧩 Output of This Component**

Once Component 4 is implemented, Aboki.xyz now has:

- a functional P2P marketplace
- escrow enforcement
- safe dual-confirmation swaps
- dispute handling
- automated settlement
- consistent logs

This is the engine that makes Aboki **trustless**, **safe**, and **automated**.

---

```
[Next: Component 5 — Hybrid Settlement (Crypto → Bank)](#component-5-hybrid-settlement-crypto--bank)
```
