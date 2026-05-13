# Bluebird Stag — Sample Investor Microsite

A public, single-page investor microsite for **201–215 Stag Industrial Blvd** (Lake St. Louis, MO) — a closed Bluebird syndication used as a sales sample of the Bluebird investor-microsite product offered to other CRE principals.

This is a sister repo to [`bluebird-wedgeway`](https://github.com/Leivascody/bluebird-wedgeway): same template, same visual system, populated with a different deal and with the 506(b) access gate removed so anyone can view it.

---

## What's in here

```
.
├── index.html          ← the entire site (all CSS + JS inline, single file)
├── images/             ← 21 property photos + favicon set + OG image (~14 MB)
├── video/              ← 3 drone videos: hero loop, mid-page break, gallery flyover (~36 MB)
├── README.md           ← you are here
├── .gitignore
└── .nojekyll           ← tells GitHub Pages to serve the file tree as-is, no Jekyll
```

Total repo size: ~50 MB. Comfortably under GitHub Pages' 1 GB soft limit and 100 MB per-file hard limit (largest file is the gallery flyover at 24 MB).

`index.html` is a single self-contained file — open it directly in a browser to preview locally:

```bash
open index.html
```

No build step. No bundler. No npm install.

---

## Three images you still need to drop in

The template references three image files that aren't in this repo. Copy these from your existing `bluebird-wedgeway` repo (they're identical assets across all Bluebird microsites):

| Path expected by `index.html` | Where to grab it |
|---|---|
| `images/bluebird-logo.png` | `bluebird-wedgeway/images/bluebird-logo.png` |
| `images/cody-leivas-headshot.png` | `bluebird-wedgeway/images/cody-leivas-headshot.png` |
| `images/kevin-mcneil-headshot.png` | `bluebird-wedgeway/images/kevin-mcneil-headshot.png` |

Quick one-liner if both repos are siblings on your machine:

```bash
cp ../bluebird-wedgeway/images/{bluebird-logo.png,cody-leivas-headshot.png,kevin-mcneil-headshot.png} ./images/
```

Until those files exist, the nav logo, footer logo, and team headshots will show as broken images. Everything else renders correctly.

### Optional cleanup before pushing

Six photo files in `images/` are leftover orphans from the first build pass (extracted from PDFs at lower resolution; replaced by the high-res 4K originals). They're not referenced anywhere in `index.html` — delete them to slim the repo by ~5 MB:

```bash
rm images/stag-aerial-overview.jpg images/stag-aerial-autumn.jpg images/stag-aerial-fall.jpg \
   images/stag-front-autumn.jpg images/stag-rear-autumn.jpg images/stag-side-autumn.jpg \
   images/stag-building-topdown.jpg images/stl-skyline-arch.jpg images/stl-rail-skyline.jpg
```

---

## Push to GitHub + enable Pages

```bash
# 1. From inside this folder (open Terminal here, or cd to it)
cd ~/Documents/Claude/Projects/"Bluebird Stag"

# (One-time cleanup if a previous attempt left a broken .git folder)
rm -rf .git

# 2. Initialize, commit, push
git init -b main
git add .
git commit -m "Initial commit — Bluebird Stag sample investor microsite"

# 3. Create the empty repo on GitHub and push (gh CLI handles both)
gh repo create Leivascody/bluebird-stag --public --source=. --remote=origin --push

# 4. Turn on GitHub Pages
gh api -X POST /repos/Leivascody/bluebird-stag/pages -f source[branch]=main -f source[path]=/
# (or via the web UI: Settings → Pages → Source: "Deploy from a branch" → main / (root) → Save)
```

Once Pages is on, the site is live at:

**https://leivascody.github.io/bluebird-stag/**

First deploy takes a couple minutes. Subsequent pushes redeploy in ~30 seconds.

### Custom domain (optional)

If you want this on something like `stag.bluebirdcre.co` or `deals.bluebirdcre.co`:

1. In your DNS, add a `CNAME` record pointing the subdomain to `leivascody.github.io`.
2. Create a file in the repo root named `CNAME` (no extension) containing just the bare domain on one line:
   ```
   stag.bluebirdcre.co
   ```
3. Commit, push. In GitHub → Settings → Pages, set the custom domain field to match. Enable "Enforce HTTPS" once the SSL cert provisions (a few minutes).

---

## Asset inventory

### Photography — 4K drone (12 aerials)
Source: 90 unique 4K (4000×2250) drone shots from Bluebird's April 2025 due-diligence flight, stored at `Bluebird Stag Industrial STL/Photos/`. Resized to 2000px wide and quality-86 JPEG for web (~500 KB each).

| File | Subject |
|---|---|
| `stag-aerial-hero.jpg` | Hero — front-side angle, full building + rear dock context |
| `stag-aerial-front.jpg` | Front facade with parking and STAG signage |
| `stag-front-wide.jpg` | Wide front view, full parking footprint |
| `stag-aerial-context.jpg` | Wide submarket context |
| `stag-aerial-side.jpg` | Front-side with road foreground |
| `stag-loading-docks.jpg` | Rear loading — all 8 dock-high doors |
| `stag-rear-loading-aerial.jpg` | Wider rear angle |
| `stag-loading-with-truck.jpg` | Rear loading with truck/trailer at dock |
| `stag-side-yard.jpg` | Side angle, adjacent yard storage |
| `stag-rear-side.jpg` | Side from rear with road context |
| `stag-back-corner.jpg` | Back corner view |
| `stag-rear-clean.jpg` | Clean rear elevation |

### Photography — interior (6 shots)
Source: ~85 iPhone shots from on-site walk-through, also at `Photos/`. Resized to 1200px wide.

| File | Subject |
|---|---|
| `stag-interior-rexel-showroom.jpg` | Rexel USA showroom + conf. room |
| `stag-interior-rexel-warehouse.jpg` | Rexel USA pallet racking + safety signage |
| `stag-interior-usfabric.jpg` | U.S. Fabric Solutions retail showroom |
| `stag-interior-warehouse.jpg` | Active warehouse with forklift + racking |
| `stag-interior-electrical.jpg` | AllCom network/electrical infrastructure room |
| `stag-interior-office.jpg` | Tenant office build-out (~70% office finish) |

### Drone video (3 clips, all H.264 MP4 1080p)
Source: 3 raw drone videos in `Photos/` (DJI_0329/0330/0331 — total 861 MB at 35 Mbps). Re-encoded for web with `ffmpeg libx264 -preset veryfast -crf 25-26 -movflags +faststart`.

| File | Used in | Length | Size | Notes |
|---|---|---|---|---|
| `video/stag-hero-loop.mp4` | Hero background (autoplay, muted, loop) | 15 s | 3.0 MB | Trimmed from DJI_0330, audio stripped |
| `video/stag-aerial-detail.mp4` | Mid-page video break (click to play) | 59 s | 7.9 MB | Full DJI_0331, with audio |
| `video/stag-drone-full.mp4` | Gallery featured flyover (click to play) | 60 s | 24 MB | Trimmed from DJI_0329 (111s source), with audio |

### Other
- `images/og-image.jpg` — 1200×630 social-link preview image (cropped from `stag-aerial-front`)
- `images/favicon-{16,32,256}.png` + `favicon.ico` — gold "B" on navy

---

## Where the deal data came from

All deal numbers, tenant info, NOI projections, and capital-structure detail were extracted from the actual deal documents in Dropbox:

- `Bluebird Stag Industrial STL/Investment Memo/BB Stag Investment Memorandum.pdf`
- `Bluebird Stag Industrial STL/OM & Marketing/OM - 201-215 Stag Industrial Blvd Saint Charles (STL).pdf`
- `Bluebird Stag Industrial STL/Valuations/V3 (Base) Bluebird Stag.xlsx`
- `Bluebird Stag Industrial STL/Escrow/Stag_Industrial Closing_Checklist_ and critical dates.docx`
- `Bluebird Stag Industrial STL/Loan Package/Term Sheet - Stag and Trustone - x.pdf`
- `Bluebird Stag Industrial STL/Loan Package/AM Schedule - Bluebird Stag LLC.pdf`

---

## How this differs from `bluebird-wedgeway`

This is a **public sales sample** — no investor access gate. Visitors land directly on the deal page. The Wedgeway template's full-screen gate (name + email + invitation code + three click-through attestations + Google Sheets lead capture) was removed for this version because the Stag deal is closed and this microsite is meant to be freely shareable as a marketing asset.

Other differences:
- Real on-site interior photography (Rexel, U.S. Fabric, AllCom) in a dedicated "Inside the Building" section between Tenants and Market — Wedgeway is aerial-only at this stage of pre-close diligence
- Returns calibrated to a 5-year hold (Stag) versus 10-year (Wedgeway)
- Sales-CTA repointed at prospective sponsor clients ("Want a microsite like this?") rather than LP investors

If you want to spin up a new gated microsite for an active offering, start from `bluebird-wedgeway` — the gate, lead-capture wiring, and `private-banner` are all intact there.

---

## Editing tips

The whole site is one file with three logical layers:

1. **CSS** (lines ~30–1060) — design system. Don't touch unless you want to change the visual identity. Note: the dead `.access-gate` / `.gate-card` CSS rules near the top are inert leftovers from the gated template — they never apply because the gate HTML is removed. Harmless, ~120 lines, kept to make diffing against `bluebird-wedgeway` easier.
2. **HTML body** (lines ~1080–1830) — content sections. Section headings are commented (`<!-- ============== HERO ============== -->` etc.) for easy navigation.
3. **JavaScript** (bottom) — animations, NOI chart, gallery + lightbox, investor calculator. Three things you'd actually update per-deal:
   - `noi` and `noiLabels` arrays in the **NOI Chart** block — paste in your model's NOI by year.
   - `LP_EQUITY`, `LP_OP`, `LP_CAP` in the **Investor Calculator** block — total LP equity raise, operating distributions per year, capital-event distributions per year.
   - `aerialPhotos` and `interiorPhotos` arrays in the **Gallery** block — list of filenames (no extension, no path).

The investor-calculator math automatically pro-rates against the chosen investment size (the buttons across the top), so you only need to enter the model's $1,550K-equity-base distributions once.
