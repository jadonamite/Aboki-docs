---
# **Final Project Summary (Aboki V2 – Technical Architecture)**

Aboki V2 is a **fintech-grade, gasless, passkey-based crypto payment system** running entirely on the **Base blockchain**.
It blends real-world mobile money design with Web3 infrastructure — without exposing any crypto complexity to the user.

The architecture is intentionally **lean**, **scalable**, and **MVP-ready**, with a clear path toward full production.
---

## ** Core Principles**

### **1. No Crypto Friction**

- No seed phrases
- No gas fees
- No ETH holdings
- No blockchain knowledge required

Users interact like they would with **Opay**, **PalmPay**, or **Chipper** — but every transaction settles on Base.

---

### **2. Deterministic Identity**

Using:

- Passkeys
- Social username resolution
- Coinbase Smart Wallets

Every user is tied to a secure, non-custodial smart account.

---

### **3. Real-World Payment Flows**

USDC can move:

- P2P (username → username)
- Merchant → customer (QR codes)
- Crypto → Bank (Naira payout)

Aboki is instantly compatible with actual Nigerian financial infrastructure.

---

### **4. Minimal Backend, Maximum On-Chain**

All value-transfer logic is:

- executed on-chain
- gasless
- signed with biometrics
- verified with passkeys

Backend only handles:

- identity
- username lookup
- settlement references
- notifications

No private keys ever touch the backend.

---

## ** Component-by-Component Summary**

### **1. Smart Account Infrastructure**

- Coinbase Smart Wallet
- Passkey-secured deterministic addresses
- Base Mainnet only
- Gas sponsorship configured at the policy level

### **2. Authentication & Identity**

- Passkeys (FaceID / Fingerprint)
- Social username resolution layer
- Postgres profile table
- Instant wallet creation upon first login

### **3. Balance Management**

- USDC & ETH fetched directly from-chain
- Auto-refresh every 30 seconds
- Cached balance for instant load
- USD valuation using public price APIs

### **4. Peer-to-Peer Transaction Engine**

- Username → Address resolver
- On-device transaction construction
- Gasless UserOps
- Optimistic UI for instant feedback
- Works with external wallets too

### **5. Hybrid Settlement (Crypto → Bank)**

- FIAT rail: Paycrest / Kotani
- USDC → Provider USDC address
- Provider → Naira bank settlement via NIBSS
- Webhook status callbacks
- No custody held by Aboki

### **6. Merchant Payment System**

- Dynamic/Static QR codes
- Deep linking: `aboki://pay?...`
- Merchant = normal user with a business profile
- Manual “cash out” via Component 5
- No auto-settlement for MVP

### **7. Gasless Infrastructure (Paymaster)**

- Coinbase Paymaster sponsorship
- USDC.transfer whitelisting
- Daily/monthly spend caps
- Device + biometrics enforced before sponsorship
- Optional multi-paymaster redundancy

---

## ** What This Architecture Enables**

### **A. A Complete Payment Experience**

- Send money
- Receive money
- Pay merchants
- Cash out to banks
- Authenticate with FaceID
- See balances instantly
- Never buy gas

### **B. Lightning-fast UX**

Optimistic UI + gas sponsorship = feels like a Web2 mobile money app.

### **C. Scalability**

Each component is independently upgradeable:

- Replace Paycrest with a better provider
- Add more tokens in future
- Add merchant dashboards later
- Add loyalty / rewards
- Add full KYC if needed

### **D. Clean MVP Path**

This system can be shipped **in 8–12 weeks** by a small team.

---

## ** Documentation Navigation**

Add this at the bottom:

```
[Back to Top](#final-project-summary)

[Start Again → Component 1](#component-1-smart-contract-account-infrastructure)
```

Or if each component is in a separate file:

```
[Back to Top](./V2_OVERVIEW.md)

[Start Again → Component 1](./Component_1.md)
```

---

If you want, I can now:
Format **ALL components** into standalone files
Create navigation headers for each file
Generate a **new tree** for your repository
Write a README that ties V1 + V2 together

Just tell me **“assemble the full V2 docs”**.
