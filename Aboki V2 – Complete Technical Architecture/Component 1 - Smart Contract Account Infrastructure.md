Component 1: Smart Contract Account Infrastructure
Core Concept

For the V2 MVP on Base, every user is assigned a Coinbase Smart Wallet.
This wallet behaves like a bank account, not a traditional crypto wallet — no seed phrases, no gas payments, no complexity.

Why It Matters

Traditional wallets create friction:

Users need ETH for gas

Users must learn seed-phrase security

Wallet UX feels “crypto,” not “fintech”

Coinbase Smart Wallet solves this:

✔ Gas Sponsorship (users don't pay gas)
✔ Biometric Signing (FaceID/Fingerprint)
✔ Safe, custodial-like UX without actually being custodial
✔ Deterministic wallet tied to device identity

Technical Directives
1. Integration

Use Coinbase Smart Wallet SDK as the exclusive wallet provider.

No Metamask

No WalletConnect

No EOA setups

The app is a controlled identity environment.

2. Network

Hardcode all blockchain interactions to:

Base Mainnet
Chain ID: 8453


No testnets, no switching.

3. Gas Policy (Paymaster)

Enable global gas sponsorship, so users pay zero fees.

Inside the Coinbase Developer Console:

Enable Paymaster

Sponsor all USDC.transfer calls

Set spending limits (e.g., $500/month)

User experience:
Every transaction feels like sending money in a normal fintech app.

Wallet Creation Flow

User signs in with Passkey / FaceID / Fingerprint

Coinbase SDK creates a deterministic Smart Contract Account

App stores no private keys

User can now transact gaslessly on Base

Key Implementation Checklist

 Install Coinbase Smart Wallet SDK

 Configure Base Mainnet

 Enable Paymaster sponsorship

 Trigger createPasskey on first login

 Trigger authenticate on every transaction

 Store user → wallet mapping in backend (Postgres)



 **Next:** [Component 2 — Authentication & Identity](./Component%202%20-%20Authentication%20%26%20Identity.md)
