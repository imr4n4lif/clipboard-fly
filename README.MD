# ClipboardFly

Share clipboard content between devices instantly using a PIN. No account required. End-to-end encrypted.

![ClipboardFly](assets/screenshot.png)

---

## How it works

1. Open the app on Device A, click **Host Session** — a 9-digit PIN is generated.
2. Open the app on Device B, click **Join Session**, enter the PIN.
3. Hit **Paste** on either device to sync your clipboard.

Sessions expire after 15 minutes.

---

## Running Locally

```bash
cd server
npm install
npm start
```

Then open `client/public/index.html` in your browser. No build step needed.

Update the WebSocket URL in `index.html` to point to your local server:

```js
const WS_SERVER_URL = 'ws://localhost:3000';
```

## Deploying

Deploy the `server/` folder to [Render](https://render.com) or any Node host, then update `WS_SERVER_URL` in `index.html` with your server's URL and host the HTML file statically.

---

## Security

- The PIN is hashed with SHA-256 before being sent to the server — the server never sees the raw PIN.
- The encryption key is derived client-side using PBKDF2 and never leaves the browser.
- The server only relays encrypted blobs and cannot read your clipboard content.

---

## Stack

- Frontend: Single HTML file, Web Crypto API (AES-256-GCM)
- Backend: Node.js + WebSocket (`ws`)