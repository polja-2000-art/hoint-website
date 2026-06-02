# House of Intelligence

A premium static website for **House of Intelligence**, a brand by HoZK exploring the intersection of Web3, AI, digital infrastructure, and institutional innovation.

Single-page editorial layout with calm institutional aesthetic — dark navy "vault" background, EB Garamond serif typography, thin gold accents, generous spacing.

---

## Folder Structure

```
house-of-intelligence/
├── index.html              # The entire site (HTML + CSS + JS, ~60 KB)
├── favicon.svg             # SVG favicon (modern browsers)
├── favicon-32.png          # PNG fallback favicon
├── apple-touch-icon.png    # iOS home-screen icon
├── vercel.json             # Cache headers + clean URLs config
├── README.md               # This file
└── assets/
    ├── logos/              # Wordmark + partner logos (11 files)
    │   ├── wordmark.png            # House of Intelligence wordmark (nav + footer)
    │   ├── hozk-monogram.png       # HOZK monogram in hero
    │   ├── 0g.png
    │   ├── credit-scend.png
    │   ├── cysic.png
    │   ├── kenomic.png
    │   ├── lagrange.png
    │   ├── mercuryo.png
    │   ├── optimism.png
    │   ├── sapien.png
    │   └── spearbit.png
    └── images/             # Photography + decorative imagery
        ├── about-wave.jpg
        ├── interview-lukas-sapien.jpg
        ├── interview-george-v-0g.jpg
        ├── interview-jonathan-sealcoin.jpg
        └── interview-annie-cysic.jpg
```

All asset paths are **relative** (`assets/logos/...`, `assets/images/...`). The site works as a static drop-in on any host.

---

## Deployment to Vercel via GitHub

1. **Push to GitHub**

   ```bash
   cd house-of-intelligence
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<your-org>/<repo>.git
   git push -u origin main
   ```

2. **Import on Vercel**
   - Go to <https://vercel.com/new>
   - Import the repository
   - Framework Preset: **Other** (no build step required — it's a pure static site)
   - Root Directory: leave as `.`
   - Build Command: leave empty
   - Output Directory: leave empty
   - Click **Deploy**

3. Vercel will serve `index.html` and the `assets/` folder. The included `vercel.json` adds long-cache headers to immutable assets (logos, images) and short-cache to `index.html`.

**No build configuration is required** beyond what's already in the project.

### Custom domain

In the Vercel project settings, add your domain (e.g. `houseofintelligence.xyz`) and follow Vercel's DNS instructions.

---

## Local Preview

Open `index.html` directly in a browser, or run any static server:

```bash
# Python
python3 -m http.server 8000

# Node
npx serve .
```

Visit <http://localhost:8000>.

---

## What's Included

- **Hero** — "House of Intelligence" wordmark, tagline, "A strategic platform by HOZK"
- **About** — brand statement with decorative wave imagery
- **Upcoming Events** — five editorial event rows (Tokyo / Toronto / Hong Kong / Seoul / Singapore), each opens a centered modal with full details
- **House Signals** — four interview cards linking to frame.io
- **Strategic Partnerships** — auto-scrolling logo marquee (pauses on hover)
- **Request Access** — contact section with email + Telegram
- **Footer** — wordmark, attribution, copyright

### Interactions

- Smooth-scroll anchor navigation (About / Events / Signals)
- **Mobile menu** — hamburger reveals slide-down panel (About / Events / Signals / Contact); closes on link tap, Escape key, or button tap
- **Event modal** — tap any event row to open; closes via ×, backdrop click, or Escape; locks body scroll; restores focus
- **Marquee** — pauses on hover, seamless infinite loop
- **Reveal-on-scroll** — sections fade in as they enter viewport
- **Link hover states** — gold underline sweeps across email, Telegram, interview titles

---

## Performance

- **index.html**: ~60 KB (was 1.7 MB with base64-embedded images)
- **Total assets**: ~720 KB (11 logos + 5 images)
- All off-screen images marked `loading="lazy"` and `decoding="async"`
- Wordmark preloaded for instant hero render
- Google Fonts (EB Garamond + Tenor Sans) loaded with `display=swap`
- `vercel.json` sets aggressive cache headers on `assets/*` (1 year, immutable)

### Lighthouse expectations

When deployed to Vercel with the included cache headers, the site should score in the high 90s for Performance, Accessibility, Best Practices, and SEO. Largest Contentful Paint is driven by the hero wordmark which is preloaded.

---

## Known Placeholders (require manual edit before launch)

Two non-blocking placeholders remain in `index.html`. The site renders and is fully usable as-is — these don't break anything, just leave specific actions inert until real values are filled in:

### 1. Luma registration URLs

In the `EVENTS` JavaScript object near the bottom of `index.html`, four of the five events have `luma: ''` and one (Toronto) has `luma: 'PASTE_LUMA_LINK'`. The "Register via Luma" button in each event modal is **automatically dimmed and non-clickable** until you replace the placeholder with a real Luma event URL.

Search for `PASTE_LUMA_LINK` and the empty `luma: ''` entries; replace with the Luma URLs as events go live.

### 2. Two interview cards link to frame.io share root

In the `SIGNALS_INTERVIEWS` array, two interview cards (Jonathan · Sealcoin, Annie · Cysic) point to the frame.io share root rather than specific video URLs. When the dedicated video URLs are available, search for `https://next.frame.io/share/15122251` in `index.html` and replace those two entries with the specific video URLs.

---

## Browser Support

Tested in modern Chromium, Safari, and Firefox. Uses `aspect-ratio`, `clamp()`, CSS custom properties, and `IntersectionObserver` — all supported in browsers from 2020 onwards.

---

## Editing Content

The HTML is hand-written and readable. Most content can be edited in place:

- **Event data**: `EVENTS` object in the `<script>` block (look for `webx`, `toronto`, etc.)
- **Interview data**: `SIGNALS_INTERVIEWS` array
- **Partner logos**: `<div class="partner-logo">` blocks inside `.partners-track` (note: the track contains **two copies** of the logo set for the seamless loop — update both)
- **Hero copy & taglines**: inside `<header class="threshold">`
- **About copy**: inside `<section class="doctrine">`
- **Contact details**: inside `<section class="request">`

---

## Credits

Design and engineering: in collaboration with Claude.
Brand: House of ZK (HoZK), Ontario, Canada.

© MMXXVI · All rights reserved.
