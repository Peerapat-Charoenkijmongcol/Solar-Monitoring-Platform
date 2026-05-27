# Deploying to GitHub Pages

This guide shows three ways to publish `index.html` so it runs in a browser via a public URL.

---

## Option A — GitHub Web UI (easiest, no command line)

1. **Create the repository**
   - Go to <https://github.com/new>
   - Repository name: `repco-solar-monitoring` (or any name you prefer)
   - Visibility: Public (required for free Pages on personal accounts). If your account is on a paid plan, Private also works.
   - Tick **Add a README file** → Click **Create repository**

2. **Upload the files**
   - On the repo home page click **Add file → Upload files**
   - Drag `index.html` and `README.md` from your computer
   - Scroll down → Commit message: `Initial dashboard` → Click **Commit changes**

3. **Turn on GitHub Pages**
   - In the repo, go to **Settings** (top right of the repo nav)
   - Left sidebar → **Pages**
   - Under **Source**, select **Deploy from a branch**
   - Branch: `main`, Folder: `/ (root)` → Click **Save**
   - Wait ~30–60 seconds, then refresh the Pages settings page

4. **Open your dashboard**
   - The URL appears at the top of the Pages settings: `https://<username>.github.io/repco-solar-monitoring/`
   - Open it. You should see the dashboard.

---

## Option B — Git command line

If you already have Git installed and an SSH key set up:

```bash
# 1. Clone the empty repo (after creating it on GitHub)
git clone https://github.com/<username>/repco-solar-monitoring.git
cd repco-solar-monitoring

# 2. Drop the files in
cp /path/to/index.html .
cp /path/to/README.md .

# 3. Commit and push
git add .
git commit -m "Initial dashboard"
git push origin main

# 4. Enable Pages — open Settings → Pages and choose "Deploy from a branch / main / /(root)"
```

After ~1 minute the dashboard is live at `https://<username>.github.io/repco-solar-monitoring/`.

---

## Option C — GitHub Actions (auto-deploy on every push)

If you want every commit to automatically redeploy, create a workflow file:

`.github/workflows/deploy.yml`
```yaml
name: Deploy to Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - id: deployment
        uses: actions/deploy-pages@v4
```

Then in repo Settings → Pages, change **Source** to **GitHub Actions**.

---

## After deployment

### Custom domain (optional)
If you own a domain like `monitoring.repco.com`:
1. Settings → Pages → **Custom domain** → enter `monitoring.repco.com` → Save
2. At your DNS provider, add a CNAME record pointing to `<username>.github.io`
3. Wait for the SSL cert to provision (usually 5–30 min)

### Updates
Just push (or upload) a new `index.html` to the repo — GitHub Pages re-deploys automatically within a minute.

### Versioning snapshots
The platform's saved configurations (KPI Mapping, Alert Thresholds, Status Mapping) are stored in the browser's **localStorage** per origin. They survive page reloads but are not synced across users or devices. For shared/team config, use the **Export / Import JSON** buttons in each config tab to keep snapshots in the repo.

---

## Troubleshooting

**"404 / Page not found" after enabling Pages**
- Wait another 1–2 minutes; first deployment is slower
- Confirm the file is named exactly `index.html` (lowercase)
- Check Settings → Pages shows a green ✅ "Your site is live"

**Charts don't show / blank dashboard**
- The page loads scripts from CDN. If the network blocks `cdn.jsdelivr.net`, `cdnjs.cloudflare.com`, `unpkg.com` or `fonts.googleapis.com`, vendor the libraries locally and update the `<script src=…>` tags

**Want to keep it private**
- GitHub Pages on free accounts requires a public repo. For private hosting, use:
  - GitHub Pages with a Pro/Team/Enterprise plan (supports private Pages)
  - Or any static host: Netlify, Vercel, Cloudflare Pages, S3 + CloudFront

---

## Quick checklist
- [ ] Created GitHub repo
- [ ] Uploaded `index.html` (and `README.md`)
- [ ] Settings → Pages → Source set to `main / (root)`
- [ ] Opened `https://<username>.github.io/<repo>/` and saw the dashboard
- [ ] Bookmarked the URL
