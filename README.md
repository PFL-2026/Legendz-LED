# PFL Activation Page — Reusable Template

A single-file HTML activation page (originally built for **PFL × Legendz**) that can be re-skinned for any partner brand by editing one block at the top of `index.html`.

## Folder structure

```
pfl-activation-template/
├── index.html
├── README.md
└── assets/
    ├── favicons/        ← favicon.ico + PNG sizes + webmanifest
    └── images/          ← hero crowd shot + product shots (swap per brand)
```

## How to customise for a new brand

Open `index.html` in any text editor. At the very top of the `<head>` you'll see a clearly marked block:

```js
window.ACTIVATION_CONFIG = {
  brandName:        "Legendz",
  brandAccent:      "#3aa0ff",
  ...
};
```

Edit the values inside that block — **nothing else needs to change**. Everything below it (title tag, social meta, the topbar, hero, activation copy, stat strip, commercials, footer) is auto-populated from these values when the page loads.

### What each field controls

| Field | What it changes |
|---|---|
| `brandName` | Partner name shown in topbar, body copy, etc. |
| `brandAccent` | Glow colour behind the LED wristband product shot and the highlighted activation title |
| `brandAccentText` | Lighter shade used for the partner name in the topbar lockup |
| `pageTitle` | Browser tab title + Open Graph / Twitter share title |
| `pageDescription` | Meta description for SEO |
| `ogDescription` | Longer description shown on social shares (Slack, iMessage, LinkedIn) |
| `appShortName` | iOS / Android home-screen short name |
| `eventName` | Event name shown in topbar, kicker, commercials |
| `eventTerm` | "Term" row in the commercials block (e.g. "One (1) Event Test") |
| `territory` | Territory row in the commercials block |
| `exclusivity` | Exclusivity row in the commercials block |
| `eyebrow` | Small red label above the hero headline |
| `heroTitleLine1` | First line of the big hero headline — supports HTML (e.g. `<span class="red">word</span>` for a red accent word) |
| `heroTitleLine2` | Second line of the hero headline, rendered in ghost-outline style |
| `heroSubcopy` | Paragraph beneath the headline |
| `ctaNote` | Small line of text next to the "Jump to the Commercials" button |
| `activationTitle` | Title of the collapsible activation block |
| `activationTag` | Small tag on the right side of the activation block (e.g. `★ Test · PFL San Diego`) |
| `activationIntro` | Lead paragraph inside the activation block — supports HTML |
| `activationBullets` | Array of bullet points — each entry supports HTML for **bold** etc. |
| `stats` | Array of 4 stats — each `{ num, label }` |
| `imgHeroCrowd` | Filename of the wide arena/crowd image inside `assets/images/` |
| `imgProductBand` | Filename of the product-on-its-own shot inside `assets/images/` (PNG with transparent bg works best) |
| `imgProductWrist` | Filename of the on-wrist close-up inside `assets/images/` |
| `activationFee` | Big red fee number (e.g. `$30,000`) |
| `activationFeeNote` | Small line under the fee |
| `footerLine` | Left side of the footer — supports HTML |
| `footerNote` | Right side of the footer |

### Swapping images

Drop your new images into `assets/images/` and reference their filenames in the config. Recommended sizes / formats:

- **Hero crowd shot** — wide JPG, around 1600×400, dark/moody works best (it gets faded at top + bottom via a CSS mask)
- **Product band** — PNG with transparent background, ~800×600. The page adds a glow behind it using `brandAccent`
- **Product on wrist** — close-up JPG, around 1200×900

You can keep the existing `lz-*.jpg` files for brands where the LED wristband visual still applies, or replace them entirely.

### Changing the favicon

If you want a new favicon per brand, replace the files in `assets/favicons/` with the same filenames. A free tool like [realfavicongenerator.net](https://realfavicongenerator.net) will produce the full set from a single source image.

---

## Hosting on GitHub Pages

Each new activation page is best deployed as its own repo for a clean URL.

### One-time setup (per new brand page)

1. **Create a new repo** on GitHub (public). Name it something like `pfl-brandname-activation`.
2. **Upload the files**: either drag the whole folder contents (`index.html`, `README.md`, `assets/`) into the GitHub web UI, or push from the command line:
   ```bash
   cd pfl-brandname-activation
   git init
   git add .
   git commit -m "Initial activation page"
   git branch -M main
   git remote add origin https://github.com/<your-username>/pfl-brandname-activation.git
   git push -u origin main
   ```
3. **Enable Pages**:
   - Go to **Settings → Pages**
   - Under **Build and deployment → Source**, choose **Deploy from a branch**
   - Select branch `main` and folder `/ (root)`, then click **Save**
4. After ~30 seconds your page will be live at:
   ```
   https://<your-username>.github.io/pfl-brandname-activation/
   ```

### To update the live page later

Just commit and push changes to `main` — GitHub Pages rebuilds automatically.

### Custom domain (optional)

In **Settings → Pages → Custom domain**, enter your domain (e.g. `legendz.pfl.com`), then add the CNAME record at your DNS provider pointing to `<your-username>.github.io`.

---

## Producing a new brand package from this template

Quickest workflow:

1. Copy the whole `pfl-activation-template/` folder
2. Rename it to `pfl-<brandname>-activation/`
3. Open `index.html`, edit the `ACTIVATION_CONFIG` block, save
4. Replace images in `assets/images/` if needed
5. Create a new GitHub repo, push, enable Pages

That's it — the rest of the page reflows automatically.

---

## Local preview

To preview locally before pushing, open a terminal in the project folder and run:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080` in your browser. (Opening `index.html` directly via `file://` will work too, but the webmanifest may show console warnings.)
