# Taru — setup guide

Content planning + sales dashboard for the Taru team. Works on desktop and phone, synced through one GitHub repo, no server required. "Log in" as a Member (with the shared code) to edit, or as a Guest to just view.

## 1. Create the repo

- Go to github.com → **New repository**
- Name it e.g. `taru-app`
- Public is fine (matches how this app is designed — see the note at the bottom)
- Click **Create repository**

## 2. Create a personal access token

Only people who need to **edit** (Members) need to do this. Guests can skip it entirely.

- Go to github.com → click your profile photo → **Settings**
- Scroll to **Developer settings** (bottom of left sidebar)
- **Personal access tokens → Fine-grained tokens → Generate new token**
- Name it `taru`
- Under **Repository access**, choose **Only select repositories** → pick `taru-app`
- Under **Permissions → Repository permissions**, set **Contents** to **Read and write**
- Generate the token and copy it somewhere safe — GitHub only shows it once

## 3. Upload the app files

Upload these into the repo root:

- `index.html`
- `manifest.json`
- `icon.svg`
- `sw.js`

Then go to repo **Settings → Pages → Source: Deploy from a branch → Branch: main, folder / (root) → Save**.

GitHub gives you a URL like `https://yourusername.github.io/taru-app/`.

> Don't create a `data/taru-data.json` file yourself — the app creates it automatically the first time someone with a token saves.

## 4. Open it and connect sync (once per device)

- Open the GitHub Pages URL
- You'll land on a login screen — choose **Member** (enter the code: `Taru123`, then pick or add your name) or **Guest** (view only, no code needed)
- Tap the **sync button** (top right, next to the stats) → fills in the setup form
- Enter:
  - GitHub username
  - Repo name → `taru-app`
  - Branch → `main`
  - Token → the one from step 2 (**Members only** — Guests can leave this blank and still see the latest data, just can't push changes)
- Save — content categories, sales months, and the member list now sync to `data/taru-data.json` in the repo

Repeat step 4 on other devices (same repo/branch), or use **"Copy setup link"** after saving to send a one-tap setup link to a teammate — opening it once configures their device automatically. (If the link includes your token, only send it to people you trust with edit access — same as sharing a password.)

## 5. Install it like an app

- **Android/Chrome**: open the URL → menu → **Add to Home screen**
- **iPhone/Safari**: open the URL → Share button → **Add to Home Screen**
- **Desktop (Chrome/Edge)**: open the URL → address bar → install icon → **Install**

## Notes

- **Member code (`Taru123`) is not real security.** It just keeps friends from accidentally editing when they're only browsing. Anyone who knows the code (or has a token) can edit. That's expected here since privacy wasn't a requirement — same spirit as the rest of this app.
- **Sync logic**: every change saves locally instantly (works offline, even without sync set up). ~1.5s after a change it pushes to GitHub if a token is configured and you're online. On login/app open it pulls the latest version first.
- **Conflict handling is whole-board, last-edit-wins** — if two people edit different things while both offline, whichever syncs *last* becomes the saved version for everyone, not a smart merge of both edits. Fine for casual use with a few people; just know it's not merge-safe for simultaneous heavy editing.
- **Images** (category previews, sales proof screenshots) are stored directly inside the synced JSON file as embedded data. Keep them reasonably sized — a handful of modest photos is fine, but many large, high-res images across many categories can make the sync file large and slow to push/pull.
- Logging out clears the "current user" from that device's browser, showing the login screen again. It doesn't delete any data.
- Theme (light/dark) and preview mode (image/text) are remembered per device, not synced.
