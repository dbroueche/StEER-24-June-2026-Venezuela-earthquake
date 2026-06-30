# Venezuela Earthquake — Imagery + Intensity Viewer

A single-file web map for the **June 24, 2026 Venezuela earthquake doublet** (M7.2 foreshock + M7.5 mainshock). It overlays three open data sources in the browser, with no backend:

- **Vantor (Maxar) Open Data** satellite scenes — toggleable footprints and per-scene Cloud-Optimized GeoTIFF imagery, streamed via HTTP range requests.
- **USGS ShakeMap** Modified Mercalli Intensity (MMI) contours — an independent toggle per event.
- **crisisvenezuela.org** building-damage points — color-coded by damage state, filterable, with full source-cited metadata on click.

Everything is one `index.html`. It fetches all data live, so viewers always see current information.

## Live demo

https://dbroueche.github.io/StEER-24-June-2026-Venezuela-earthquake/

## Features

- Toggle image **footprints** on the map; the imagery filter also filters footprints.
- Toggle **individual scenes** independently; opacity slider; "fit" to any scene.
- **Two intensity toggles** (mainshock / foreshock). Mainshock loads by default as the high-intensity envelope.
- **Damage points** colored by `nivel` (total collapse / severe / partial / damage), with per-state filter checkboxes and live counts.
- Points reported with people **trapped** are ringed; **approximate (geocoded)** locations are drawn with a dashed outline so they aren't mistaken for precise addresses.
- Click any footprint or damage point for details; damage popups link back to the original sources.

## Run locally

It must be served over HTTP — opening the file directly (`file://`) breaks cross-origin data fetches.

```bash
# Python (use the Anaconda Prompt if `python` isn't found)
python -m http.server 8000

# …or Node, with no install
npx serve
```

Then open `http://localhost:8000/` (or whatever port is shown).

## Data sources & licenses

| Layer | Source | License |
|---|---|---|
| Satellite imagery | [Vantor Open Data](https://www.vantor.com/company/open-data-program/) | **CC-BY-NC-4.0 (non-commercial)** |
| Shaking intensity | [USGS ShakeMap](https://earthquake.usgs.gov/data/shakemap/) | Public domain (US Gov) |
| Building-damage points | [crisisvenezuela.org](https://crisisvenezuela.org/api) | CC-BY-4.0 |
| Basemap | OpenStreetMap / CARTO | ODbL / CARTO terms |

**Because the imagery is non-commercial, this tool and any deployment of it must remain non-commercial.** Keep the attribution footer intact.

The crisis data is aggregated open-source intelligence corroborated across sources — it is **not** official confirmation and does not replace authorities. Each point carries its source count and links so it can be verified.

## Contributing

Contributions are welcome.

- **Issues** — report bugs or request features via the Issues tab.
- **Pull requests** — fork, make your change, open a PR. Since the whole app is one file, most changes are small and easy to review.
- **Good first additions** — a pre/post-event imagery swipe compare, a "minimum sources" slider for the damage layer, vendored (offline) dependencies, or retargeting `CONFIG` to other events.

Please keep the non-commercial constraint and attribution in mind for any change that touches the imagery or footer.

## Code license

The **code** in this repository is released under the [MIT License](./LICENSE). Note that the MIT license covers the source only — the **data** displayed is governed by the licenses in the table above (notably the non-commercial imagery).
