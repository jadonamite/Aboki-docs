# **Component 2: Authentication & Identity**

## **Core Concept**

Authentication is the bridge between a human user and their blockchain identity.
V2 eliminates seed phrases entirely and replaces them with:

- **Passkeys (WebAuthn)**
- **Biometric Authentication (FaceID / Fingerprint)**

This makes the wallet feel like a normal mobile banking app.

---

## **Mechanism 1: Biometric Passkeys**

### **Primary Auth Flow**

1. User taps **“Sign Up / Login”**
2. Device prompts **FaceID / Fingerprint**
3. Coinbase SDK validates and returns the deterministic wallet
4. No passwords
5. No recovery phrases
6. No traditional crypto UX

#### **Why This Works**

- Passkeys are synced with iCloud Keychain / Google Password Manager
- Security is hardware-level
- Eliminates user error
- Extremely Nigerian-friendly (biometrics are widely used)

---

## **Mechanism 2: Social Identity Layer**

Humans understand **@usernames**, not `0xABCD...`.

We establish a mapping layer:

```
user_id  ↔  @username  ↔  smart_wallet_address
```

### **Core Database (Postgres)**

Table: `users`

| Column         | Description             |
| -------------- | ----------------------- |
| username       | Unique handle `@chioma` |
| display_name   | Human name (optional)   |
| wallet_address | Coinbase smart wallet   |
| created_at     | Timestamp               |

---

## **Lookup API**

The frontend should resolve usernames via:

```
GET /api/resolve-username?handle=@chioma
```

Return:

```json
{
  "wallet_address": "0xDEF123..."
}
```

Used in:

- P2P transfers
- Merchant QR payments
- Request money flows

---

## **Technical Directives**

### **Frontend**

- Trigger `createPasskey()` and `authenticate()` flows through Coinbase SDK
- Sync wallet + username after signup
- Always store usernames in lowercase for uniqueness

### **Backend**

- Enforce 1:1 uniqueness for usernames
- Validate handles using regex: `^[a-z0-9_]{3,15}$`
- Provide a fast lookup API (<20ms)

---

## **User Onboarding Flow (Combined)**

1. User opens app
2. Presses **Login / Create Account**
3. Passkey prompt appears
4. SDK auto-derives smart wallet
5. User picks a username
6. Username stored + mapped
7. Home screen loads with their wallet & balance

---

## **Why This Matters**

Component 2 creates the **human interface** for the system:

- No seed phrase
- No addresses
- No passwords
- Just biometrics + @username

This is **fintech-grade onboarding**, not crypto onboarding.

---

Here is your next-component link to attach at the bottom:

**Next:** [Component 3 — Balance Management](./Component%203%20-%20Balance%20Management.md)
