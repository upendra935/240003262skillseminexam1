This repository is a small Vite-based React project. The intent of this file is to give AI coding agents the minimal, actionable context needed to make correct, useful edits quickly.

Key facts
- Project type: Vite + React app located under `skill/`.
- Entry points: `skill/index.html` loads `skill/src/main.js`. The React app root component is `skill/src/app.jsx` (exported default App) but `main.js` currently renders a non-React demo; be careful when changing the bootstrap.
- Routing: `skill/src/app.jsx` uses `react-router-dom` with nested routes. `Dashboard.jsx` uses `<Outlet/>` and contains links to `profile` and `settings`.
- Build & dev: use npm scripts in `skill/package.json`:
  - `npm run dev` — start Vite dev server
  - `npm run build` — build for production
  - `npm run preview` — preview production build

Project-specific patterns and gotchas
- Mixed bootstrap: `skill/src/main.js` is the default Vite/vanilla JS demo and mounts DOM directly. The React app lives in `skill/src/app.jsx` but is not currently imported by `main.js`. When adding or changing React rendering, update `skill/index.html` or `skill/src/main.js` to mount `App` into `#app`.
- File locations to check when changing routing or navigation:
  - `skill/src/app.jsx` (routes)
  - `skill/src/Dashboard.jsx`, `Profile.jsx`, `Settings.jsx` (route targets)
- Static assets: `skill/index.html` references `/vite.svg`; `main.js` imports `javascript.svg` from `src/`. Keep paths starting with `/` as Vite resolves them to project root.
- No dependency list for React/router is present in `package.json` (devDependencies only include Vite). If you add React or react-router, update `skill/package.json` and install (npm install react react-dom react-router-dom) — or ask before adding packages.

Examples of common edits
- To render the React App on dev server, replace `skill/src/main.js` content with an import of `App` and ReactDOM.render (or createRoot) and ensure `skill/index.html` still has `<div id="app"></div>`.
- To add a new nested route under Dashboard: add the new component file in `skill/src/`, import it in `app.jsx`, and add `<Route path="new" element={<New/>} />` inside the `/dashboard` Route.

Where to look when tests or builds fail
- Build errors: run `npm run build` in `skill/` and inspect Vite output. Typical fixes are missing imports, wrong asset paths (leading `/` vs relative), or missing dependencies.
- Runtime errors: check console for missing React runtime or ReactDOM errors — indicates React isn't installed or bootstrap mismatch between `main.js` and `app.jsx`.

Minimal editing contract for AI changes (keep PRs small)
- Inputs: file path(s) and a short description of behavior change.
- Outputs: updated source files and (if adding deps) an updated `skill/package.json` with exact package versions.
- Error modes: avoid adding new dependencies without updating package.json. If you must, add a short note explaining why.

Quick references
- App root: `skill/src/app.jsx`
- Vite entry: `skill/src/main.js` and `skill/index.html`
- Routes: `skill/src/Dashboard.jsx`, `Profile.jsx`, `Settings.jsx`
- Dev/build commands: `skill/package.json` scripts

If anything in this doc is ambiguous, ask a human before making dependency or bootstrap changes.

---
If you'd like, I can also:
- Patch `skill/src/main.js` to mount the React `App` (small, safe change), or
- Add `react` and `react-router-dom` to `skill/package.json` and install them (requires permission).
