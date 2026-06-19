# Data Analyst Placement Sprint — Tracker

A single self-contained page (`index.html`) that tracks your placement-prep roadmap: checkboxes per resource, a progress bar per phase, an overall progress gauge, and a "Day X / 30" counter — all saved automatically in your browser, no backend required.

## Deploy on GitHub Pages with GitHub Actions

1. **Create a new repository** on GitHub, e.g. `placement-tracker`.
   - On a free GitHub account, the repo needs to be **Public** for Pages to work (unless you're on GitHub Pro/Team/Enterprise).

2. **Push this folder's contents to the repo root.** From inside this unzipped folder:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: placement sprint tracker"
   git branch -M main
   git remote add origin https://github.com/<your-username>/placement-tracker.git
   git push -u origin main
   ```

3. **Turn on GitHub Actions–based Pages.** In your repo on GitHub:
   `Settings → Pages → Build and deployment → Source` → select **GitHub Actions**.

4. **Trigger the deploy.** The workflow at `.github/workflows/deploy.yml` runs automatically on every push to `main`. You can also trigger it manually from the **Actions** tab → select the workflow → **Run workflow**.

5. **Open your live page** at:
   ```
   https://<your-username>.github.io/placement-tracker/
   ```
   (It can take a minute or two after the first successful run for the URL to go live.)

## How progress tracking works

- Every checkbox writes a key to your browser's `localStorage` — nothing is sent to any server, and nothing is shared between devices/browsers.
- The "Day X / 30" badge stores the date you first opened the page and counts forward from there.
- The **RESET** button (top right) clears all saved progress and restarts the day counter from today — it asks for confirmation first.
- Clearing your browser's site data/cache will also reset progress, since it's the same storage mechanism.

## Customizing the roadmap

Open `index.html` and find the `PHASES` array near the bottom of the file. Each phase is an object with a `title`, a `days` label, and an `items` array. Each item supports:

```js
{ id: "unique-id", title: "Resource name", desc: "Optional description", link: "https://...", linkLabel: "Open resource", tag: "CORE" }
```

`tag` can be `SETUP`, `CORE`, `PRACTICE`, `PROJECT`, `MAINTAIN`, or `STRETCH` — each has its own badge style. Add, remove, or reorder items freely; the checkboxes, progress bars, and gauge all rebuild themselves from this array automatically. Keep each `id` unique, or saved progress for that item won't persist correctly.
