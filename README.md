# Pteronautics

The home page of the Pteronautics family: free, open-source aerospace engineering that runs in the browser.

| Program | What it's for | Site |
| --- | --- | --- |
| **Pteronautics Atlas** | Learn how the physics works, one concept at a time, with a live visual for every concept | https://blazingdrako.github.io/pteronautics-atlas/ |
| **Pteronautics Works** | Design whole vehicles on the same validated solvers, coupled together, with requirements checked live | https://blazingdrako.github.io/pteronautics-works/ |

This repository is only the umbrella site: https://blazingdrako.github.io/pteronautics/

## How the live figures work

GitHub Pages serves this site and the two programs from the same origin, side by side:

```
https://blazingdrako.github.io/pteronautics/          this site
https://blazingdrako.github.io/pteronautics-atlas/    Atlas
https://blazingdrako.github.io/pteronautics-works/    Works
```

So the page imports the programs' own modules at run time, from `../pteronautics-atlas/` and `../pteronautics-works/`:

- **From Atlas:** the line-art preview of every tool (`js/previews.js`), the same drawings as the Atlas home page.
- **From Works:** Kestrel solved by the coupling graph and drawn in 3D, the slider demo that drives the real graph, and an mfoil airfoil solution run in a Web Worker.

Nothing is copied or screenshotted, so the page always shows the programs as they are. If either program cannot be reached, or a module it imports moves, those figures fall back to text and every link still works. If you rename or move these files in Atlas or Works, update `js/site.js`:

- Atlas: `js/previews.js` (export `PREVIEWS`)
- Works: `src/ui/dom.js`, `src/engine/graph.js`, `src/analyses/fixedWing.js`, `src/model/seeds.js`, `src/model/vehicle.js`, `src/ui/view3d.js`, `src/ui/planform.js`, `src/ui/graphView.js`, `src/ui/airfoilLab.js`, `src/workers/client.js`, `src/adapters/airfoil.js`

The tool names and one-line summaries of Atlas's tools are written into `js/site.js` (the `ATLAS_TOOLS` list), following the Atlas home page; update them there when Atlas gains a tool.

The design tokens and fonts are copied from the family's shared design system (`css/pteronautics.css`, from Works, whose tokens come from Atlas), and the preview styles from Atlas (`css/previews.css`), so the site keeps its look on its own.

## Run it locally

Clone the three repositories side by side, then serve them together:

```bash
git clone https://github.com/BlazingDrako/pteronautics
```

```bash
git clone https://github.com/BlazingDrako/pteronautics-atlas
```

```bash
git clone https://github.com/BlazingDrako/pteronautics-works
```

```bash
python3 pteronautics/serve.py
```

It opens http://localhost:8780/pteronautics/ and serves only those three folders, only to this computer. Without the two programs beside it, the page still works and shows its fallbacks.

## Publishing

GitHub Pages serves the `main` branch as it is (Settings → Pages → Deploy from a branch: `main`, root). `.nojekyll` makes Pages serve the files without processing them.

## License

Copyright (C) 2026 Andrew Aguiar. Free software under the GNU General Public License v3.0 (see `LICENSE` and `COPYRIGHT`). The bundled fonts are under the SIL Open Font License (see `assets/fonts/`).
