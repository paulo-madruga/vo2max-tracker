# VO₂ MAX Interval Trainer

Personal VO₂ max interval protocol app with GitHub-backed session storage and PWA support.

---

## Setup: ~10 minutes total

### Step 1 — Create the GitHub repo

1. Go to [github.com/new](https://github.com/new)
2. Name it `vo2max-trainer` (or anything you like)
3. Set to **Private** (recommended — your training data)
4. Check **"Add a README file"** so the repo initializes
5. Click **Create repository**

---

### Step 2 — Enable GitHub Pages

1. In the repo, go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Branch: `main`, folder: `/ (root)`
4. Click **Save**
5. GitHub will show you a URL like `https://yourusername.github.io/vo2max-trainer`
   — this is your app URL

---

### Step 3 — Upload the app files

Upload these three files to the root of the repo (drag & drop in the GitHub UI or use `git`):

```
index.html
manifest.json
sw.js
```

For `git`:
```bash
git clone https://github.com/yourusername/vo2max-trainer.git
cd vo2max-trainer
# copy the 3 files here
git add .
git commit -m "Initial app deploy"
git push
```

---

### Step 4 — Create the data file path

The app writes session data to `data/sessions.json`. Create an empty placeholder:

1. In the GitHub UI, click **Add file → Create new file**
2. Name it `data/sessions.json`
3. Content: `[]`
4. Commit directly to main

---

### Step 5 — Create a Personal Access Token

1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)**
2. Click **Generate new token (classic)**
3. Note: `vo2max-trainer access`
4. Expiration: `No expiration` (or 1 year, your call)
5. Scopes: check **`repo`** (full repo access — needed to read/write `data/sessions.json`)
6. Click **Generate token**
7. **Copy it immediately** — GitHub only shows it once

---

### Step 6 — Configure the app

1. Open your app at `https://yourusername.github.io/vo2max-trainer`
2. The setup modal will appear on first load
3. Enter:
   - **Token**: the `ghp_...` token from Step 5
   - **Repo**: `yourusername/vo2max-trainer`
   - **Data file path**: `data/sessions.json`
4. Click **Save & Connect**

The app will immediately pull any existing sessions and sync after each workout.

---

### Step 7 — Install as PWA on iPhone

1. Open the app URL in **Safari** (PWA install only works in Safari on iOS)
2. Tap the **Share** button (box with arrow)
3. Scroll down and tap **"Add to Home Screen"**
4. Name it `VO₂MAX`
5. Tap **Add**

The app will appear on your home screen and open fullscreen, no browser chrome.

---

## How session data works

- Sessions are stored in `data/sessions.json` in your GitHub repo
- The app pulls from GitHub on load and pushes after every completed session
- A local cache (`localStorage`) is maintained for offline fallback
- If you change devices: install the app, enter the same token + repo, it pulls your full history

---

## Progression rules

| Condition | Recommendation |
|---|---|
| 0 drops, all intervals complete | Clean session — repeat once more before advancing |
| 2 consecutive clean sessions | Advance speed 0.1–0.2 mph **or** move to next protocol |
| 1 drop logged | Stay at current speed, repeat |
| ≥ 2 drops logged | Hold speed, do not increase |

Speed drops are logged with: interval number, time-of-drop into interval, speed before and after.

---

## Protocol ladder

| # | Protocol | Structure | Advancement trigger |
|---|---|---|---|
| 1 | FOUNDATION | 3 × 3 min / 3 min rec | 2 clean sessions |
| 2 | STANDARD | 4 × 4 min / 3 min rec | 2 clean sessions |
| 3 | COMPRESSED | 4 × 4 min / 2.5 min rec | 2 clean sessions |
| 4 | ADVANCED | 5 × 4 min / 2.5 min rec | Increase speed only |

---

## Updating the app

To update the app in the future (new features, fixes):
```bash
# Replace index.html with the new version, then:
git add index.html
git commit -m "App update"
git push
```
GitHub Pages deploys automatically within ~1 minute. Session data in `data/sessions.json` is unaffected.
