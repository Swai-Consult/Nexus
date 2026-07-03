# ProEstate v3 — Firebase Setup Guide

## What you need
- A Google account (Gmail is fine)
- 15 minutes

---

## Step 1 — Create a Firebase Project

1. Go to https://console.firebase.google.com
2. Click **Add project**
3. Name it `ProEstate` (or anything you like)
4. Disable Google Analytics (not needed) → **Create project**

---

## Step 2 — Create the Database

1. In the left sidebar click **Build → Realtime Database**
2. Click **Create Database**
3. Choose **Singapore** or the closest region to South Africa
4. Select **Start in test mode** → **Enable**

---

## Step 3 — Get Your Config

1. Click the ⚙️ gear icon (top left) → **Project settings**
2. Scroll down to **Your apps** → click the **</>** (Web) button
3. Register app name: `ProEstate` → **Register app**
4. Copy the `firebaseConfig` object — looks like:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "proestate-xxxxx.firebaseapp.com",
  databaseURL: "https://proestate-xxxxx-default-rtdb.firebaseio.com",
  projectId: "proestate-xxxxx",
  storageBucket: "proestate-xxxxx.appspot.com",
  messagingSenderId: "12345678",
  appId: "1:12345678:web:abcdef"
};
```

---

## Step 4 — Paste config into index.html

Open `index.html` in Notepad (or any text editor).

Find this section near the top of the `<script>` block:

```js
var FIREBASE_CONFIG = {
  apiKey:            "PASTE_API_KEY",
  authDomain:        "PASTE_PROJECT_ID.firebaseapp.com",
  ...
```

Replace each `PASTE_...` value with your real values from Step 3.

Save the file.

---

## Step 5 — Publish to GitHub Pages

1. Create a free account at https://github.com
2. Click **New repository** → name it `proestate` → **Public** → **Create**
3. Upload ALL files from this folder (index.html, manifest.json, sw.js, icons/, SETUP.md)
4. Go to **Settings → Pages → Source → main branch → / (root)** → **Save**
5. Wait ~60 seconds → your URL appears: `https://YOUR-USERNAME.github.io/proestate/`

---

## Step 6 — Share with your team

- **Admin**: open the URL, click Agency Admin, create your account
- **Agents**: share the same URL, they select Property Agent
- **Contractors**: share the same URL, they select Contractor

Everyone installs it on their device:
- **Chrome (desktop)**: address bar → install icon (⊕) on the right
- **Android**: menu → Add to Home Screen
- **iPhone/iPad**: Safari → Share → Add to Home Screen

---

## Security (optional but recommended)

Once live, lock down the database so only your app can write to it:

Firebase Console → Realtime Database → **Rules** → paste:
```json
{
  "rules": {
    ".read":  true,
    ".write": true
  }
}
```

For tighter security, ask your developer to add Firebase Authentication rules.

---

## Backup

All data lives in Firebase. To export a snapshot:
- Admin login → **Backup / Restore** → **Export Backup (.json)**
- Save to Google Drive or email to yourself monthly
