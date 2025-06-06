---
# 🐋 Warlot — Decentralized, Pay-As-You-Use Storage Gateway on Sui & Walrus
---

## 🌐 Overview

Warlot is a next-generation decentralized node storage platform built on the Sui blockchain and integrated with the Walrus storage system. It combines blockchain integrity, efficient file storage, and automated epoch lifecycle management to provide:

- 🔐 **Blockchain-backed file metadata** and ownership
- 💸 **Pay-as-you-use billing**, paying only for storage epochs used
- 🔄 **Automatic renewal and expiration** handling
- 🗝️ **Secure API key and encryption management**
- 👥 **User registration and identity management**
- 🔧 **Admin controls for uploads and file replacement**
- 🔐 **Signature-based middleware for secure API access**

---

## 🎯 What Warlot Achieves

| Feature                        | Description                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------------------ |
| Decentralized storage          | Files are represented on-chain with tamper-proof metadata ensuring verifiable ownership.         |
| Pay-as-you-use billing         | Users pay only for the storage epochs their files occupy, with easy renewal or deletion options. |
| Automatic lifecycle management | Automated renewal via bots, and marking files deletable when expired or replaced.                |
| Secure API & encryption keys   | API and encryption keys are generated, signed, and verified securely on-chain.                   |
| User registration & management | Wallet-based user registration with email and name verified and securely stored off-chain.       |
| Signature-protected API routes | Middleware verifies wallet ownership and API keys against on-chain state to secure endpoints.    |
| Walrus storage integration     | Efficient file storage management leveraging the Walrus CLI with epoch and deletability support. |

---

## 🏗️ Application Components & Architecture

### 1. **Warlot Core Contract**

- Manages user registration, wallet balances, blob metadata, and lifecycle.
- On-chain governance of blobs, epochs, and billing.
- Emits events for indexing and off-chain tracking.

### 2. **renewbot 🤖 — Blob Renewal Automation**

- Automated On-chain and off-chain service monitoring blob expiration epochs.
- Automatically renews blob storage or marks blobs as deletable.
- Reduces manual overhead, ensuring continuous storage.

### 3. **sui-indexer 🔍 — Blockchain Event Indexing**

- Watches the Sui blockchain for Warlot contract events (blob creation, renewal, removal).
- Maintains an up-to-date index for fast querying and analytics.
- Powers dashboards and user queries.

### 4. **testnet walrus 🦦 — Testnet Deployment & Utilities**

- Holds main logic of the Renew and sync operation of the system
- Stores user funds for renewal and syncing
- Stores Users Blob Obj

### 5. **warlots-publisher 📤 — Upload & Management Client**

- tooling for users and admins to upload, replace, and remove files.
- Handles API key management, cryptographic signing, and metadata generation.
- Interfaces with both Warlot smart contract and Walrus storage backend.

---

## 🔄 End-to-End Workflow

1. **User Registration**
   User registers using their wallet address, provides verified email & name. Warlot creates an on-chain user profile and wallet.

2. **File Upload**
   Using walrus-publisher, user uploads a file to Walrus storage, generating metadata and signing the upload with their API key.

3. **Blob Creation on-chain**
   Metadata including file hashes, epoch info, and owner references are written to Warlot contract, establishing blockchain provenance.

4. **Storage Billing & Epoch Management**
   Warlot tracks file storage epochs; user pays according to usage.

5. **Automated Renewal via renewbot**
   renewbot monitors blobs nearing expiration and renews storage or flags files for deletion.

6. **Event Indexing via sui-indexer**
   Indexer listens to blockchain events, updates off-chain indexes to power dashboards and queries.

7. **Admin Controls**
   Admin users can replace or delete files, monitor system health, and control storage parameters.

8. **User Queries & API Access**
   Signature-based middleware ensures only authorized wallets with valid API keys can access user or blob data.

---

## 🔐 Security & Access Control

- API keys are generated and cryptographically signed with the user’s wallet.
- Middleware verifies wallet ownership and on-chain data before allowing API requests.
- All blob metadata on-chain is immutable, ensuring transparency and tamper resistance.

---

## 📁 Folder Structure Overview

```
/
 warlot                      # Core Sui smart contracts for user and blob management
 _  ^
├── renewbot/               # Automated renewal bot service for blob lifecycle management
├── sui-indexer/            # Sui blockchain event indexer to track Warlot events
├── testnet-walrus/         # Warlot Sui UnderLining contract
├── warlot-publisher/       # tools for upload & management
├── warlottable/            # Table schema helpers and indexing utilities
└── README.md               # This documentation file
```

---

## 🧩 Integration Points

| Component        | Role                                        | Communication                      |
| ---------------- | ------------------------------------------- | ---------------------------------- |
| Warlot Contract  | On-chain logic, metadata, user/wallet state | Sui blockchain                     |
| renewbot         | Automated lifecycle & renewal               | Reads blockchain, calls contract   |
| sui-indexer      | Event indexing & query engine               | Listens to blockchain events       |
| testnet walrus   | Deployment and environment management       | CLI & scripts                      |
| warlot-publisher | User/admin upload & management interface    | Calls Warlot contract & Walrus CLI |
| Walrus Storage   | Actual file storage backend                 | CLI invoked by warlot-publisher    |

---

## 📝 Summary

Warlot unites the power of the Sui blockchain with the efficient storage capabilities of Walrus to deliver a truly decentralized, pay-as-you-go cloud storage platform. Its modular architecture involving renewbot, sui-indexer, testnet walrus, and walrus-publisher ensures scalability, security, and seamless user experience — from file upload to automated lifecycle management.

---
