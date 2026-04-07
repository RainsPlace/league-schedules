[GitHub-Pages-Hosting-Guide.md](https://github.com/user-attachments/files/26545532/GitHub-Pages-Hosting-Guide.md)
# Hosting Google Apps Script Web Apps on GitHub Pages
### A Step-by-Step Guide — No Banner, No Login Required

---

## Why We Do This

Google Apps Script web apps show an annoying banner at the top that says
*"This application was created by a Google Apps Script user."*
There is no way to remove it from within the app itself.

The solution is to host just the **HTML file** on GitHub Pages (free),
while the **data still comes from Google Apps Script** running silently
in the background. Users only ever see the clean GitHub Pages URL.

```
User opens GitHub Pages URL
        ↓
HTML page loads instantly (no banner)
        ↓
Page quietly fetches data from your GAS /exec URL
        ↓
Tournaments / leaderboard data appears
```

---

## Part 1 — Your First App (What You Already Did)

### Step 1 — Create a GitHub Account
Go to **github.com** and sign up for a free account.
Remember your username — it becomes part of every app URL.

### Step 2 — Create a New Repository
1. Click the **+** button (top right) → **New repository**
2. **Repository name** — use a short, lowercase, no-spaces name.
   Examples: `league-schedules`, `eb-leaderboard`, `nw-leaderboard`
3. Set visibility to **Public** (required for free GitHub Pages)
4. Check **Add a README file** (makes setup easier)
5. Click **Create repository**

### Step 3 — Upload Your HTML File
1. Inside your new repository, click **Add file** → **Upload files**
2. Rename your HTML file to **`index.html`** before uploading
   *(This tells GitHub Pages which file to show when someone visits the URL)*
3. Drag the file in, or click to browse for it
4. Scroll down and click **Commit changes**

### Step 4 — Turn On GitHub Pages
1. Click **Settings** (tab at the top of the repository)
2. Click **Pages** in the left sidebar
3. Under **Source**, change the dropdown from *None* to **main**
4. Leave the folder set to **/ (root)**
5. Click **Save**
6. Wait about 60 seconds, then refresh the page
7. A green banner will appear showing your live URL:
   ```
   https://YOUR-USERNAME.github.io/REPO-NAME/
   ```

### Step 5 — Test It
Click the link GitHub shows you. Your app should open with no banner.
If it shows a 404 error, wait another minute and try again —
GitHub Pages can take 1–2 minutes to go live the first time.

---

## Part 2 — Adding More Apps

**Yes — every app can be named `index.html`.**
Each app lives in its own repository, so the names never conflict.

### Example — Three Apps, Three Repos

| App | Repository Name | Live URL |
|-----|----------------|----------|
| League Schedules | `league-schedules` | `woodp.github.io/league-schedules/` |
| Early Bird Leaderboard | `eb-leaderboard` | `woodp.github.io/eb-leaderboard/` |
| Nordic Warriors Leaderboard | `nw-leaderboard` | `woodp.github.io/nw-leaderboard/` |

Each repo has one file called `index.html` — no conflicts.

### Steps to Add Each New App

1. Go to **github.com** → click **+** → **New repository**
2. Give it a new unique name (see table above for examples)
3. Check **Public** and **Add a README file**
4. Click **Create repository**
5. Click **Add file** → **Upload files**
6. Upload your HTML file — make sure it is named **`index.html`**
7. Click **Commit changes**
8. Go to **Settings** → **Pages** → Source: **main** → Save
9. Wait 60 seconds → your new URL is live

Repeat for every additional app. Each one is completely separate.

---

## Part 3 — Updating an App After You Make Changes

When you edit your HTML file in Notepad++ and want to push the update live:

1. Go to **github.com** → open the repository for that app
2. Click on **index.html** in the file list
3. Click the **pencil icon** (Edit this file) — top right of the file view
4. Select all the text and delete it (`Ctrl+A` then `Delete`)
5. Open your updated `index.html` in Notepad++, select all (`Ctrl+A`),
   copy (`Ctrl+C`), and paste into the GitHub editor (`Ctrl+V`)
6. Scroll down → click **Commit changes**
7. The live site updates automatically within about 60 seconds

> **Tip:** You can also use the **Upload files** button to re-upload the file
> and overwrite the old one — whichever feels easier.

---

## Part 4 — How the Two Pieces Work Together

It helps to understand what lives where:

| Piece | Where It Lives | What It Does |
|-------|---------------|--------------|
| `index.html` | GitHub Pages | What users see — the interface, tabs, styling |
| `MasterWebApp.gs` | Google Apps Script | Fetches tournament data from casino.org API |
| `WEBAPP_URL` | Inside `index.html` | The address that connects the two pieces |

The `WEBAPP_URL` inside each HTML file must point to **that app's own**
Google Apps Script `/exec` deployment URL. Different apps have different
GAS deployments, so each `index.html` has a different `WEBAPP_URL`.

---

## Part 5 — Quick Reference Checklist

Use this every time you host a new app:

- [ ] HTML file renamed to `index.html`
- [ ] `WEBAPP_URL` inside the file is filled in with the GAS `/exec` URL
- [ ] New GitHub repository created (Public)
- [ ] `index.html` uploaded to the repository
- [ ] GitHub Pages turned on: Settings → Pages → Source: main → Save
- [ ] Waited ~60 seconds and tested the live URL
- [ ] URL bookmarked / shared with league members

---

## Troubleshooting

**The page shows a 404 error**
Wait 1–2 more minutes and refresh. GitHub Pages takes time to activate
the first time. If it still shows 404 after 5 minutes, double-check that
GitHub Pages is turned on in Settings → Pages.

**The page loads but shows no data / loading spinner stays forever**
The `WEBAPP_URL` inside `index.html` is either empty or incorrect.
Open the file, find the line that says `const WEBAPP_URL = ''` and make
sure the GAS `/exec` URL is pasted between the quotes.

**The data is old / not updating**
Click the Refresh button inside the app. If you also set up the
`refreshCache` trigger in Apps Script (every 30 minutes), the data
will update automatically in the background.

**I edited the file but the live site didn't change**
GitHub Pages caches aggressively. After committing, wait 60 seconds,
then do a hard refresh in your browser: `Ctrl + Shift + R` (Windows)
or `Cmd + Shift + R` (Mac).
