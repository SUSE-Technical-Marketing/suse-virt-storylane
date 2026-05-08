# SUSE Virtualization — Interactive Demo Hub

A static HTML site that gives prospects and customers a guided, hands-on introduction to SUSE Virtualization. Six interactive Storylane demos, each paired with a step-by-step instructions panel, covering the platform from first login to a running Kubernetes cluster on HCI.

## Contents

```
index.html          — Demo hub landing page
lab.html            — Split-screen lab environment (iframe + instructions panel)
schedule.html       — Internal 5-day recording and delivery schedule
css/style.css       — Marketing site styles
css/lab.css         — Lab environment styles
img/suse-logo.png   — SUSE chameleon + wordmark (transparent PNG)
docs/
  poc-guide-v1.7.0.md     — SUSE Virtualization POC Guide reference
  suse-virt-0-to-hero.md  — Full lab guide and recording scripts
```

## Run locally

The site is plain HTML — no build step, no dependencies, no Node.js required.

### Option 1: Python (built into macOS and most Linux distros)

```bash
git clone https://github.com/SUSE-Technical-Marketing/suse-virt-storylane.git
cd suse-virt-storylane
python3 -m http.server 8080
```

Open [http://localhost:8080](http://localhost:8080) in your browser.

### Option 2: Node.js `serve`

```bash
git clone https://github.com/SUSE-Technical-Marketing/suse-virt-storylane.git
cd suse-virt-storylane
npx serve .
```

### Option 3: VS Code Live Server extension

1. Open the cloned folder in VS Code.
2. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension.
3. Right-click `index.html` and choose **Open with Live Server**.

### Option 4: Open the file directly

For basic browsing you can open `index.html` directly in a browser (`File → Open` or drag the file in). The lab page (`lab.html`) embeds the Storylane demo in an iframe, which requires a server for the embed to load correctly — use any option above when testing labs.

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

- **Left** — Storylane interactive demo (iframe)
- **Right** — Step-by-step instructions panel with a progress indicator and checkboxes

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
