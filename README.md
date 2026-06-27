# VaultAuth — WebAuthn Demo

A working biometric authentication demo using the **WebAuthn / FIDO2** browser API. Register once with your fingerprint (or Face ID / Windows Hello), then sign in instantly — no passwords.

## Live Demo

Deploy on Vercel (see below) to get a working HTTPS URL.

## How it works

1. **Register** — Enter a username, your device prompts for biometric, a public key credential is created and saved to `sessionStorage`
2. **Login** — Your device verifies your biometric and returns a cryptographic assertion
3. **Success** — In production you'd verify the assertion server-side; here we trust the browser for demo purposes

## Files

```
index.html    ← entire app (HTML + CSS + JS, no dependencies)
vercel.json   ← sets Permissions-Policy header for WebAuthn
```

## Deploy to Vercel

```bash
# 1. Push to GitHub
git init
git add .
git commit -m "WebAuthn demo"
gh repo create webauthn-demo --public --push

# 2. Go to vercel.com → Add New Project → Import repo → Deploy
```

That's it. Vercel auto-detects the static HTML file.

## Run locally

```bash
# Python
python -m http.server 8080
# open http://localhost:8080

# or Node
npx serve .
# open http://localhost:3000
```

> WebAuthn requires `localhost` or valid HTTPS — it won't work on `file://` or self-signed certs.

## Production notes

- Credentials are stored in `sessionStorage` (cleared on tab close) — demo only
- In a real app, send the attestation/assertion to your backend and verify the signature using [@simplewebauthn/server](https://simplewebauthn.dev) (Node) or [py_webauthn](https://github.com/duo-labs/py_webauthn) (Python)
- The `vercel.json` sets the required `Permissions-Policy` header so WebAuthn works correctly when embedded

## Browser support

Chrome, Safari, Firefox, Edge — all major browsers on desktop and mobile.
