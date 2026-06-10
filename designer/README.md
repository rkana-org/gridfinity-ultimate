# Gridfinity Ultimate

A static, fully client-side parametric configurator for [Gridfinity](https://gridfinity.xyz)
bins. It builds a JSON configuration you can paste into — or open directly in — the
companion Onshape model.

The app is plain HTML + CSS + React (via global UMD builds), with the UI written as
JSX. There is **no application server**: the published site is just static files.

---

## Project layout

| Path | Role |
|------|------|
| `index.html` | Dev entry point — loads React + Babel from a CDN and the `.jsx` sources directly, for fast iteration. **Single source of truth for the page markup.** |
| `logic.js` | Pure, framework-free model/serialisation logic (`window.GF`). |
| `ui.jsx` | Shared primitives + icons (`window.Icon`, `Section`, `Field`, …). |
| `DividerEditor.jsx` `Controls.jsx` `JsonPanel.jsx` `App.jsx` | UI modules, each exposed on `window.*`. |
| `styles.css` | Design tokens + component styles. |

Every module uses the **global-script pattern** (`window.X = X`, no ES `import`/`export`).
That is what lets the production build transpile each file in place without a bundler.

---

## Development

Open `index.html` in a browser (or any static server). It loads
`@babel/standalone` and compiles the JSX on the fly — no build step, just edit and
refresh. This path is intentionally dependency-free for authoring.

## Onshape model versioning

The "Open in Onshape" button targets a **version-pinned** model link,
defined by `ONSHAPE_VERSION` / `ONSHAPE_BASE` at the top of `JsonPanel.jsx`. When a new
model version ships, bump **both** constants together so existing configs keep working
against a known-good version.
