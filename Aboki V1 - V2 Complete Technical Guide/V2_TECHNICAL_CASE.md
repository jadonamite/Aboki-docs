# Aboki V1 → V2 Architecture

## Part 3: Why V2 Works (Where V1 Couldn’t)

---

# 1. Persistent Balances → Stickiness

Users maintain a **stored balance** inside Aboki.  
This creates:

- Daily engagement
- Habit formation
- Reason to return

---

# 2. P2P Network Effects

Every new user makes the system more valuable.  
Payments feel instant and free.

---

# 3. Multiple Revenue Streams

V2 monetizes:

- Hybrid bank settlements
- Merchant processing fees
- Premium features
- Float
- Future: savings, lending, cross-border

---

# 4. Abstraction of Blockchain Complexity

Users never see:

- Gas fees
- Approve transactions
- Transaction hashes
- Seed phrases

Massive TAM expansion.

---

# V2 Data Flow

Privy Sign-in
→ Embedded Wallet
→ Smart Account Deployment
→ Username Mapping
→ User Funds Account
→ Index & Cache Balances

---

# P2P Transaction Flow

- Resolve @recipient
- Create UserOperation
- Paymaster sponsors gas
- Bundler sends to EntryPoint
- Smart account executes transfer
- Notify sender + receiver

---

# Hybrid Settlement Flow (USDC → NGN Bank)

- User → Escrow
- Backend → Paycrest
- Paycrest → NIBSS
- Escrow releases on success
- Auto-refund on failure

---

# Technical Unlocks

## ERC-4337 Account Abstraction

Enables:

- Programmable wallets
- No private-key EOA limitations
- Gasless UX
- Smart recovery flows

## Passkeys (Ideation)

Biometric-secured on-device signing.  
Yes: **Passkeys are possible in Web3** using WebAuthn + MPC wallets.

---

### 👉 Continue to V1 vs V2 Comparison\*\*

[V1 VS V2 COMPARISON.md](./V1_VS_V2_COMPARISON.md)
