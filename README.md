# Road Clearance v1.0 (build 12)

A lightweight Trimble Connect 3D Viewer extension to temporarily display selected road surface objects at a positive vertical offset for visual clearance inspection.

## Install / update

1. In the existing `jagkr1/road-clearance` GitHub repository, replace root-level `index.html` and `manifest.json` with these files and commit.
2. Ensure GitHub Pages is serving the `main` branch, root folder.
3. Update the registered manifest URL in Trimble Connect to `https://jagkr1.github.io/road-clearance/manifest.json?v=12`.
4. Fully reopen the 3D Viewer if an older version is cached. The technical log in **Advanced · Diagnostics** should say `v1.0`.

## For users

1. Select road surface objects from one model in the 3D Viewer.
2. Enter clearance height in centimetres.
3. Click **Show clearance surface**.
4. Use **Update height** to change the displayed offset, or **Remove preview** to clear it.

A small status line communicates readiness, errors and completion. Detailed object logs and manual diagnostic tools are hidden inside **Advanced · Diagnostics**.

## Scope and limitations

- Temporary visualization only; the original model is not intentionally moved or hidden.
- No certification of clearance or automated clash measurement.
- Bounding-box-based ID scanning is bounded; unusually large/sparse models may require validation, and visually checking for extra raised geometry remains necessary.
- This release changes user interface and messaging; object enumeration, copy creation, offset and visibility filtering remain based on the v0.11 implementation.
