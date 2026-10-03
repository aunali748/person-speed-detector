# Person Detector — Speed + Human vs Object 🎥

Browser-based person detection app. Detects **persons**, estimates their **speed**, and shows the **difference between a real person and other objects**.

Built by SAITAMA. Runs 100% locally in the browser — no video is uploaded anywhere.

## How to run

Just open `index.html` in a modern browser (Chrome/Edge recommended), or host via GitHub Pages.

> Camera requires **HTTPS** or **localhost**. `file://` works for the page, but `getUserMedia` may be blocked — use GitHub Pages or `npx serve`.

## What it does

- 🎥 Live webcam person detection (TensorFlow.js + COCO-SSD)
- 🟩 Green boxes = **real person** (class `person`) with ID, confidence & live speed
- 🟧 Orange boxes = **other objects** (chair, bottle, cell phone…) — clearly labeled as *not a person*
- 📏 Speed per person: **px/s** + rough **km/h** estimate (box height ≈ 1.7 m reference)
- 📊 Side panels: person list with speeds vs object list with labels/confidence

## Controls

- **Start camera & detection** — begins webcam + AI loop
- **Stop** — stops camera and clears tracks

## Human vs object — how it tells the difference

| | Real person | Object |
|---|---|---|
| Model class | `person` | anything else (`chair`, `bottle`, …) |
| Box color | green | orange |
| Tracking & speed | yes (centroid tracked across frames) | no — listed only |
| Panel | "Detected persons" | "Other objects" |

## Tech

- TensorFlow.js + COCO-SSD from CDN (no install)
- Single HTML file, no build step
- Centroid tracking with speed smoothing over ~0.5 s

## Notes

- Speed in km/h is approximate — it's estimated from bounding-box size, not calibrated.
- Detection runs on-device; works offline after CDN scripts are cached (first load needs internet).
