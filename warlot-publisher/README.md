---

# Warlot Publisher

**Warlot Publisher** is a secure file publishing API with wallet-based authentication, signature verification, and admin controls for managing uploads and file replacements.

---

## API Endpoints (Base URL: `https://d328zr3eu47he6.cloudfront.net/`)

| Type      | Method | Endpoint         | Description                     |
| --------- | ------ | ---------------- | ------------------------------- |
| Public    | POST   | `/generate`      | Generate API & encryption keys  |
| Public    | POST   | `/verify`        | Verify signatures               |
| Protected | POST   | `/upload`        | Upload files (wallet + API key) |
| Protected | POST   | `/register`      | Register a new user             |
| Protected | GET    | `/user`          | Get user info                   |
| Admin     | POST   | `/admin/upload`  | Admin file upload               |
| Admin     | POST   | `/admin/replace` | Replace an existing file        |

---

## Authentication & Headers

- Wallet-based authentication required for protected and admin endpoints.
- `X-API-Key` header for protected endpoints.
- `X-Admin-Token` header for admin endpoints.
- `X-Wallet-Address` header always required to identify the wallet.

---

## Example Requests

### 1. Generate API & Encryption Keys (Public)

```bash
curl -X POST https://d328zr3eu47he6.cloudfront.net/generate \
  -H "Content-Type: application/json" \
  -d '{"address": "YOUR_WALLET_ADDRESS"}'
```

---

### 2. Register a New User (Protected)

```bash
curl -X POST https://d328zr3eu47he6.cloudfront.net/register \
  -H "Content-Type: application/json" \
  -H "X-Wallet-Address: YOUR_WALLET_ADDRESS" \
  -H "X-API-Key: YOUR_API_KEY" \
  -d '{"name": "Bob Tester", "email": "bob@example.com"}'
```

---

### 3. Admin File Upload

```bash
curl -X POST https://d328zr3eu47he6.cloudfront.net/admin/upload \
  -H "X-Admin-Token: YOUR_ADMIN_TOKEN" \
  -H "X-Wallet-Address: YOUR_WALLET_ADDRESS" \
  -H "X-To-Address: TARGET_WALLET_ADDRESS" \
  -F 'file=@/path/to/your/file.jpg' \
  -F 'epochs=53' \
  -F 'cycle=6' \
  -F 'deletable=true'
```

---

### 4. Admin Replace File

```bash
curl -X POST https://d328zr3eu47he6.cloudfront.net/admin/replace \
  -H "X-Admin-Token: YOUR_ADMIN_TOKEN" \
  -H "X-Wallet-Address: YOUR_WALLET_ADDRESS" \
  -H "X-To-Address: TARGET_WALLET_ADDRESS" \
  -H "X-Old-Object-ID: OLD_OBJECT_ID" \
  -F 'file=@/path/to/new/file.move' \
  -F 'epochs=5' \
  -F 'cycle=6' \
  -F 'deletable=true'
```

---

## Environment Variables

- `ADMIN_TOKEN` — Secure admin token used for admin routes.

---
