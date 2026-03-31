# ReadyShipper vs ShipStation — Landing Page Reference

## Overview
A competitive comparison landing page for **ReadyShipper vs ShipStation**, hosted on GitHub Pages via the repo `ch-readycloud/readyshipper-vs-shipstation`. The page's core message: merchants using ShipStation pay hidden fees (credit card surcharges, per-label costs, volume thresholds, ~8% USPS surcharge via EasyPost), while ReadyShipper charges a flat rate with zero transaction/credit card/volume fees.

## Tech Stack
- **Single file:** `index.html` (~1,076 lines)
- **CSS:** Tailwind CSS (CDN, with forms + container-queries plugins)
- **3D Visualization:** Three.js v0.164.1 (ES module via CDN importmap) + `RoundedBoxGeometry` addon
- **Fonts:** Inter (body/headlines), Caveat (handwritten annotation), Material Symbols Outlined (icons)
- **No build step** — static HTML, hosted directly on GitHub Pages

## Brand Identity
| Token | Value |
|---|---|
| Primary (green) | `#18C98D` |
| On-primary | `#ffffff` |
| Secondary (blue) | `#3b82f6` |
| Surface | `#fcfcfc` |
| On-surface (text) | `#0f172a` |
| On-surface-variant | `#475569` |
| Outline | `#cbd5e1` |
| Border radius | `1rem` default, `2rem` lg, `3rem` xl |
| Font family | Inter (all weights 300–900) |

## Page Sections (top to bottom)

### 1. Hero Section (lines 106–452)
Two-column layout:
- **Left column:** Eyebrow badge ("Data as of 04/2026"), H1 with ReadyShipper logo inline, subheadline about hidden fees, 3 green-checkmark bullet points, "Learn More" CTA button.
- **Right column (desktop only, `lg:flex`):** Interactive 3D bar graph + slider control.

### 2. Hero 3D Bar Graph (lines 145–449) — KEY ELEMENT
- **Container:** `#hero-3d-wrapper` (460px tall), contains `#hero-3d` canvas + absolutely-positioned card overlays.
- **Scene setup:** Orthographic camera at 45-degree isometric angle (`position: 6,4,6` looking at `0,1.5,0`), frustum size 4.2. Transparent background, no shadows.
- **Two bars:**
  - **ShipStation bar** (gray `#b0bcc8`, MeshLambertMaterial) — positioned at x=1.2, grows tall based on price tier.
  - **ReadyShipper bar** (green `#18C98D` with emissive glow, MeshLambertMaterial) — positioned at x=-1.2, stays short (flat pricing).
  - Both use `RoundedBoxGeometry` (width 1.4, depth 1.1, corner radius 0.05).
- **Animation:** RS bar rises fast (800ms, easeOutCubic), SS bar rises slow (3200ms, easeInOutCubic). After initial animation completes, bars smoothly lerp to slider-driven heights.
- **Card overlays:** `#card-rs` and `#card-ss` — white rounded cards showing price counters, positioned via `toScreen()` 3D→2D projection.
- **Handwritten annotation:** "No change." text + arrow SVG appears after animation, with "(we're down here)" joke text at 15K+ tier.

### 3. Volume Slider (lines 168–192)
- Range input (`#hero-volume-slider`, 0–9 steps) controlling 10 volume tiers.
- **Volume tiers (VOLUME_TIERS array):**
  | Index | Shipments | ShipStation | ReadyShipper |
  |-------|-----------|-------------|--------------|
  | 0 | 50 | $349 | $64 |
  | 1 | 100 | $399 | $64 |
  | 2 | 500 | $449 | $64 |
  | 3 | 1,000 | $599 | $64 (default) |
  | 4 | 2,000 | $699 | $64 |
  | 5 | 5,000 | $799 | $64 |
  | 6 | 7,500 | $949 | $64 |
  | 7 | 10,000 | $1,099 | $64 |
  | 8 | 15,000 | $1,349 | $64 |
  | 9 | 20,000 | $1,499 | $64 |
- Displays monthly savings and volume label. SS bar height scales proportionally to price; RS bar height = ratio of RS/SS price * SS bar height.

### 4. Trust Bar (lines 454–527)
Infinite-scroll logo carousel with CSS `@keyframes scroll`. Logos: American Hanger, CS, Dainese, Foot Locker, Original Footwear, Revolve, Blue Cross Blue Shield, CA.gov, Crocs, Red Bull. Logos duplicated for seamless loop.

### 5. Save Big / Pricing Comparison (lines 530–635)
- H2: "Save Big When Switching to ReadyShipper"
- ShipStation pricing breakdown table (tiered pricing by shipment volume)
- ReadyShipper "$64/mo flat" callout
- "No Hidden Fees" sub-section

### 6. Switching Steps (lines 662–721)
Dark section (slate-950). H2: "Switching to ReadyShipper is Easy". Three steps: Contact Form → Hands-On Setup & Migration → Go Live in a Day.

### 7. Feature Comparison (lines 724–793)
H2: "What Sets ReadyShipper Apart from ShipStation". Feature comparison grid/table.

### 8. Testimonials (lines 796–834)
H2: "What ReadyShipper Users Say". Customer testimonial cards.

### 9. Why Choose ReadyShipper (lines 837–891)
Six benefit cards: Ship for Less, Better Control Over Carrier Costs, Automate Shipping, Faster Operations, Manage Post-Purchase, Real Support.

### 10. Start Saving / Pricing CTA (lines 894–923)
H2: "Start Saving". ReadyShipper pricing display.

### 11. Contact / "Let's Talk Ship" (lines 926–994)
Dark section with contact form. H2: "Let's Talk Ship".

### 12. FAQ (lines 997–1075)
H2: "Frequently Asked Questions". Accordion-style Q&A.

## Assets
- `/logos/` directory: SVG logos (ah-logo-color, Blue-Cross-Blue-Shield, ca.gov, Crocs, cs-logo-color, dianese, foot-locker, of-logo, revolve-1, readyshipper-logo-white) + redbull-logo.jpg

## Git Info
- **Repo:** `ch-readycloud/readyshipper-vs-shipstation`
- **Hosting:** GitHub Pages
- **Latest commit:** `dce86cf` — Add "Fed up with ShipStation?" callout, rename to "Let's Talk Ship"
