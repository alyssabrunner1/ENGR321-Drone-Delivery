# Waypoint — Drone Delivery Prototype

A working front-end prototype of an autonomous drone delivery app, built for a human factors
engineering course. It demonstrates the full customer journey — **order placement → address &
drop-zone selection → pre-flight safety checks → live tracking → delivery confirmation** — as a
mobile-first web app that installs like a native app from a phone's home screen.

No real drone is controlled. All flight, weather, and airspace data are simulated client-side so
the prototype can be demonstrated live without any backend, API keys, or network dependency.

## Feature checklist (per the assignment brief)

| Requirement | Where it lives |
|---|---|
| Address & destination accuracy | **Drop Zone** step — type an address or pick a sample, then confirm the exact hover-drop point on an interactive map |
| Safe landing / hover-drop locations | **Drop Zone** map — a highlighted safe-landing area; taps outside it or inside a hazard zone are rejected with an explanation |
| Package size & weight limits | **Package** step — category presets + a weight field with a live payload meter; over-limit packages block checkout with guidance |
| Weather & wind conditions | **Review** step — a pre-flight wind check with a safe-launch threshold; a labeled demo toggle lets you show the "launch delayed" state on demand |
| No-fly zones & airspace restrictions | **Drop Zone** map — two illustrative restricted-airspace zones (a school, an airfield); selecting a point inside one is blocked |
| Customer notifications | Toast notifications + a persistent status timeline on the **Tracking** screen as the order moves through each stage |
| Delivery confirmation (photo / QR / PIN / signature) | **Package** step lets the customer pick a method; the **Confirm** screen implements all four: PIN keypad, a scannable-style QR code, a camera/file photo capture, and a signature pad |

## Human factors notes

- **Error prevention over error correction** — the map physically constrains where a drop point
  can be placed, and the package-weight meter turns amber/red before the limit is crossed, rather
  than only rejecting after submission.
- **Status visibility** — a persistent step indicator during checkout, and a full timeline with
  timestamps during tracking, so the customer always knows what stage they're in.
- **Recognition over recall** — sample addresses and package-size presets let a user complete the
  flow without having to remember or type exact values.
- **User control** — the customer chooses their own delivery-confirmation method rather than
  having one imposed, and every blocking state (over-weight, no-fly zone, high wind) explains why
  and what to do next.
- **Thumb-reachable actions** — the primary action for each step is pinned to the bottom of the
  screen, consistent with common mobile delivery/checkout apps.

## Running it locally

This is a static site — no build step, no dependencies.

```bash
cd drone-delivery-app
python3 -m http.server 8000
# open http://localhost:8000 in a browser (or your phone, on the same network)
```

## Deploying to GitHub Pages (for submission)

1. Create a new GitHub repository (e.g. `ENGR321-Drone-Delivery-Dashboard`) and push this folder
   to its `main` branch:
   ```bash
   git init
   git add .
   git commit -m "Waypoint drone delivery prototype"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
2. In the repository, go to **Settings → Pages**.
3. Under **Source**, select the `main` branch and the `/ (root)` folder, then **Save**.
4. GitHub will publish the app at:
   `https://<your-username>.github.io/<your-repo>/`
5. On a phone, open that URL and use **Add to Home Screen**
   (iOS Safari: Share → Add to Home Screen · Android Chrome: ⋮ menu → Add to Home screen) to get
   an installed-app icon and a full-screen experience.

## Demonstrating it live

- The happy path (Home → Start a New Delivery → pick an address → confirm a drop point → pick a
  package → pick a confirmation method → Review → Place Order → watch it fly → confirm delivery)
  takes about a minute end to end.
- To show the safety gating without waiting for real weather, use the **"Simulate high-wind
  delay"** toggle on the Review step — it puts the app into the blocked state instantly and
  reverts as soon as you switch it off.
- To show the no-fly-zone rejection, tap inside either shaded zone on the Drop Zone map (labeled
  in the legend) — the highlighted safe zone is the only area a real order can be placed from.

## Project structure

```
drone-delivery-app/
├── index.html      # entire app (markup, styles, and logic)
├── manifest.json   # web app manifest (installable "Add to Home Screen" metadata)
├── icons/          # app icons (192, 512, and iOS 180px)
└── README.md
```
