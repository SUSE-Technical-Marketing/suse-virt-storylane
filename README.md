# SUSE Virtualization: Interactive Demo Hub

A static HTML site that gives prospects and customers a guided, hands-on introduction to SUSE Virtualization. Six interactive Storylane demos, each paired with a step-by-step instructions panel, covering the platform from first login to a running Kubernetes cluster on HCI.

**Live site:** [https://suse-technical-marketing.github.io/suse-virt-storylane/](https://suse-technical-marketing.github.io/suse-virt-storylane/)

Every push to `main` deploys automatically via GitHub Actions.

## Contents

```
index.html          - Demo hub landing page
lab.html            - Split-screen lab environment (iframe + instructions panel)
schedule.html       - Internal 5-day recording and delivery schedule
css/style.css       - Marketing site styles
css/lab.css         - Lab environment styles
img/suse-logo.png   - SUSE chameleon + wordmark (transparent PNG)
docs/
  poc-guide-v1.7.0.md     - SUSE Virtualization POC Guide reference
  suse-virt-0-to-hero.md  - Full lab guide and recording scripts
.github/workflows/pages.yml  - GitHub Pages deployment workflow
```

## Run locally

The site is plain HTML with no build step, no dependencies, and no Node.js required.

```bash
git clone https://github.com/SUSE-Technical-Marketing/suse-virt-storylane.git
cd suse-virt-storylane
python3 -m http.server 8080
```

Open [http://localhost:8080](http://localhost:8080) in your browser.

A local server is needed for local dev because Chrome blocks `history.pushState` on `file://` origins. For sharing with anyone else, use the live GitHub Pages URL above.

## Demo overview

| # | Demo | Duration |
|---|------|----------|
| 01 | UI Orientation | 5 min |
| 02 | Create Your First VM | 10 min |
| 03 | VM Networking | 10 min |
| 04 | Storage, Snapshots + Backups | 10 min |
| 05 | Live Migration | 5 min |
| 06 | Rancher + RKE2 | 15 min |

## How the lab environment works

Each demo card on `index.html` opens `lab.html?lab=XX` in a new tab. The lab page shows:

- **Left:** Storylane interactive demo (iframe)
- **Right:** Step-by-step instructions panel with a progress indicator and checkboxes

The instructions panel can be collapsed with the **Instructions** toggle button in the top bar. Prev/Next buttons at the bottom of the panel let users move between labs without returning to the hub.

## Adding live Storylane links

Once recordings are published, update the `storylaneUrl` field for each lab in the `LABS` config object inside `lab.html`:

```js
'01': {
  title: 'UI Orientation',
  storylaneUrl: 'https://app.storylane.io/demo/YOUR_ID_HERE',
  ...
}
```

The iframe loads automatically once the URL is set. Also update the six `btn-demo` links in `index.html` if you want the card buttons to link directly to Storylane instead of the lab page.
