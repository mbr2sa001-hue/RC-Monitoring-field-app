# RC Monitoring App — Install Package

This package contains everything needed to put the RC Monitoring App online and
install it like a native app on phones and computers.

## What's inside
- `index.html` — the app itself (already has a PWA manifest + install banner built in)
- `firebase.json`, `.firebaserc` — hosting config pointed at your existing Firebase
  project (`mbr2-dashboard`), the same one the app already uses for data storage

## Why hosting is needed
The app can only show the "Install" prompt on phones/computers when it's served
over **HTTPS from a real URL** — opening the file directly from your computer
(`file://...`) will run the app fine, but Android/Chrome/Edge won't offer the
install button, and it looks unofficial to users. Since the app already talks to
Firebase project `mbr2-dashboard`, the fastest option is **Firebase Hosting** —
same project, free tier, and a real `https://` URL in a few minutes.

## 1. Deploy it (one-time setup, ~5 minutes)

You'll need [Node.js](https://nodejs.org) installed on your computer.

```bash
# Install the Firebase CLI (once, on your computer)
npm install -g firebase-tools

# Log into the Google account that owns the mbr2-dashboard project
firebase login

# From inside this folder:
firebase deploy --only hosting
```

When it finishes, it prints a **Hosting URL** like:

```
https://mbr2-dashboard.web.app
```

That URL is what you'll open on phones and computers to install the app.
(If your Firebase account manages multiple projects, run `firebase use mbr2-dashboard`
first to make sure you're deploying to the right one.)

> Don't have CLI/terminal access? You can also drag-and-drop this folder into
> [Firebase Console → Hosting](https://console.firebase.google.com/project/mbr2-dashboard/hosting)
> using "Get started," though the CLI method above is more reliable.

## 2. Install on a phone

**Android (Chrome):**
1. Open the Hosting URL in Chrome.
2. A banner "ដំឡើង App នៅលើទូរស័ព្ទ / Install RC Monitoring App" appears at the
   bottom — tap **ដំឡើង (Install)**.
3. If it doesn't appear, tap the **⋮** menu → **Add to Home screen** / **Install app**.

**iPhone / iPad (Safari):**
1. Open the Hosting URL in **Safari** (must be Safari, not Chrome, for this to work on iOS).
2. Tap the **Share** icon (square with an arrow) at the bottom.
3. Scroll down and tap **Add to Home Screen** → **Add**.
4. The app icon now appears on the home screen and opens full-screen, like a normal app.

## 3. Install on a computer (Windows / Mac / Chromebook)

**Chrome or Edge:**
1. Open the Hosting URL.
2. Look for the **install icon** (a small monitor with a down arrow) in the
   address bar, on the right side.
3. Click it → **Install**.
4. The app opens in its own window and gets added to your Start Menu / Applications
   folder / Dock, just like a desktop app.

If you don't see the install icon: click the **⋮** (Chrome) or **···** (Edge) menu →
**Save and share** / **Apps** → **Install this site as an app**.

## Notes
- The app works offline for anything already loaded, but there's no service worker
  yet, so a fresh install still needs an internet connection the first time.
- All monitoring data syncs live with the same Firebase project as the MBR2
  dashboard — no extra setup needed there.
