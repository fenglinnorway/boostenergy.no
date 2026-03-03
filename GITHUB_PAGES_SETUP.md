# How to Deploy BoostEnergy as a GitHub Pages Static Website

This guide explains how to configure this repository so that `index.html` is served as a public static website at **`https://<your-username>.github.io/boostenergy.no/`** (or a custom domain like `boostenergy.no`).

---

## Prerequisites

- A GitHub account
- This repository pushed to GitHub (public or private with GitHub Pro/Team)

---

## Step 1 — Push the Repository to GitHub

If you haven't already done so:

```bash
# From the repo root
git add .
git commit -m "Add website files"
git push origin main
```

---

## Step 2 — Enable GitHub Pages

1. Open your repository on GitHub.
2. Click **Settings** (top tab bar of the repo).
3. In the left sidebar, scroll down to **Pages**.
4. Under **Build and deployment → Source**, select **Deploy from a branch**.
5. Under **Branch**, choose `main` and set the folder to `/ (root)`.
6. Click **Save**.

GitHub will build and deploy the site. After about 60–90 seconds, a green banner will show:

> **Your site is live at `https://<your-username>.github.io/boostenergy.no/`**

---

## Step 3 (Optional) — Use a Custom Domain (boostenergy.no)

### 3a. Add the domain in GitHub Pages settings

1. In **Settings → Pages → Custom domain**, type `boostenergy.no` and click **Save**.
2. GitHub creates a `CNAME` file in the root of the `main` branch automatically.

### 3b. Configure DNS at your domain registrar

Log in to your domain registrar (e.g., Domeneshop, Cloudflare, Namecheap) and add these DNS records:

| Type  | Host / Name | Value                    | TTL  |
|-------|-------------|--------------------------|------|
| A     | `@`         | `185.199.108.153`        | 3600 |
| A     | `@`         | `185.199.109.153`        | 3600 |
| A     | `@`         | `185.199.110.153`        | 3600 |
| A     | `@`         | `185.199.111.153`        | 3600 |
| CNAME | `www`       | `<your-username>.github.io` | 3600 |

> **Note:** DNS changes can take up to 48 hours to propagate worldwide.

### 3c. Enable HTTPS

Once DNS is verified, return to **Settings → Pages** and check **Enforce HTTPS**. GitHub provisions a free Let's Encrypt certificate automatically.

---

## Step 4 — Verify Everything Works

| Check | Expected Result |
|-------|----------------|
| Open `https://boostenergy.no` | Loads `index.html` with the BoostEnergy website |
| Open `https://www.boostenergy.no` | Redirects to `https://boostenergy.no` |
| Browser padlock | Green / secure (HTTPS) |
| Language toggle | EN ↔ 中文 switches correctly |
| Mobile view | Responsive layout, hamburger menu works |

---

## Repository File Structure

```
boostenergy.no/
├── index.html                          ← Main website (all-in-one)
├── Image_20260302235622_227_2597.jpg   ← Hero background (energy storage)
├── Image_20260302235625_228_2597.jpg   ← CRRC energy storage
├── Image_20260302235628_229_2597.jpg   ← CATL/TCC containers
├── Image_20260302235630_230_2597.jpg   ← CATL factory unit
├── Image_20260302235638_232_2597.jpg   ← EVs in snow (Nordic testing)
├── Image_20260302235640_233_2597.jpg   ← Battery module (after-sales)
├── Image_20260302235643_234_2597.jpg   ← Workers at container (installation)
├── Image_20260302235646_236_2597.jpg   ← CATL battery testing
├── Image_20260302235648_237_2597.jpg   ← Crane installation
├── Image_20260302235651_238_2597.jpg   ← Battery pack on pallet
├── Image_20260302235654_239_2597.jpg   ← Large warehouse
├── Image_20260302235657_240_2597.jpg   ← Residential solar panels
├── boostenergy.pptx                    ← Source material
├── 网站要求.docx                        ← Website requirements
└── GITHUB_PAGES_SETUP.md               ← This guide
```

> The website is a **single self-contained HTML file** with all CSS and JavaScript embedded. No build tools, Node.js or npm are required — just push and deploy.

---

## Updating the Website

To update content, edit `index.html` locally, then:

```bash
git add index.html
git commit -m "Update website content"
git push origin main
```

GitHub Pages redeploys automatically within ~60 seconds after every push to `main`.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Site shows a 404 | Make sure `index.html` is in the root of the `main` branch, not in a subfolder |
| Images not loading | Confirm all image filenames in `index.html` match exactly (case-sensitive) |
| Custom domain not working | Wait up to 48 h for DNS propagation; double-check `A` records |
| HTTPS not available | Wait ~24 h after DNS verification; check for CAA DNS records blocking Let's Encrypt |
| Old content showing | Hard-refresh the browser (`Cmd+Shift+R` / `Ctrl+Shift+R`) or wait for CDN cache to clear |
