# SplitSecond

> Split it fast, settle up easy.

A no-fuss expense splitting web app for dinners, day trips, and group outings. No accounts required. Open it, add people, split the bill, share the summary — done.

**Live demo:** [split-second-weld.vercel.app](https://split-second-weld.vercel.app)

Vibe Coded with ❤️ by Laveek Garg and Abhimanyu Sirothia

---

## What it does

- **Start a split** in seconds — auto-generated name, pick your currency, add people
- **Add expenses** with four split modes: equal, shares, exact amounts, or percentage
- **Multi-payer support** — split bills where more than one person paid
- **Live sync** — share a link or QR code and collaborators join in real time
- **Summary view** — simplified "who pays whom" settlements with one-tap mark-as-paid
- **Share as image** — generate a clean summary card to send to your WhatsApp group
- **Guest mode** — no account needed, splits saved locally on device
- **Account mode** — sign up with email or Google to access splits across devices
- **Edit people** — add, remove, or rename people mid-split without breaking past expenses

---

## Stack

| Concern | Solution |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript — single file, zero build step |
| Auth | Firebase Authentication (Anonymous, Email/Password, Google) |
| Database | Firebase Realtime Database |
| Hosting | Vercel |
| Fonts | DM Serif Display, DM Sans, DM Mono (Google Fonts) |

No frameworks. No npm. No bundler. The entire app is `index.html`.

---

## Getting started

### 1. Clone the repo

```bash
git clone https://github.com/yourusername/splitsecond.git
cd splitsecond
```

### 2. Set up Firebase

1. Go to [console.firebase.google.com](https://console.firebase.google.com) and create a project
2. Enable **Authentication** → Anonymous, Email/Password, and Google sign-in methods
3. Enable **Realtime Database** → start in test mode
4. Go to **Project Settings → Your Apps** → add a web app → copy the config object

### 3. Add your Firebase config

Open `index.html` and replace the `firebaseConfig` block near the top:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT-default-rtdb.firebasedatabase.app",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

### 4. Set database security rules

In Firebase Console → Realtime Database → Rules:

```json
{
  "rules": {
    "splits": {
      "$splitId": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}
```

### 5. Run locally

No server needed — just open the file in a browser:

```bash
open index.html
```

Or use any static file server:

```bash
npx serve .
```

---

## Deploying to Vercel

### Option A — Drag and drop

1. Go to [vercel.com](https://vercel.com) → New Project
2. Drag `index.html` onto the deploy area
3. Done

### Option B — GitHub integration (recommended)

1. Push this repo to GitHub
2. Import it in Vercel — it auto-detects a static site, no build settings needed
3. Every push to `main` auto-deploys

### After deploying

Add your Vercel domain to Firebase's authorised list so Google sign-in works:

**Firebase Console → Authentication → Settings → Authorised domains** → add `your-project.vercel.app`

---

## Project structure

```
splitsecond/
└── index.html    # The entire app — HTML, CSS, and JS in one file
```

That's it. Intentionally simple.

---

## Features in detail

### Split modes
| Mode | How it works |
|---|---|
| Equal | Total divided evenly across all active people |
| Shares | Set a share count per person — 2 shares = pays twice as much as 1 share |
| Exact | Enter a specific amount for each person |
| Percentage | Enter a percentage per person — must sum to 100% |

### People management
- **Add** — new people only appear in future expenses
- **Remove** — hidden from future expenses, past calculations preserved
- **Rename** — updates everywhere including all past expenses

### Guest vs account
| | Guest | Account |
|---|---|---|
| No sign-up required | ✓ | — |
| Splits synced across devices | — | ✓ |
| Real-time collaboration | ✓ | ✓ |
| Share via link / QR | ✓ | ✓ |
| Data stored | Device only | Firebase |

---

## Design

The visual design is derived from a custom design spec (`design.md`) — warm off-white background, a single orange accent (`#E8471A`), DM Serif Display for headings, DM Sans for body, DM Mono for numbers and metadata.

Key principle: **orange is used only for active states and primary actions** — never decoratively.

---

## License

MIT
