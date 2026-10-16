# Road Clearance Preview — Trimble Connect (experimental v0.3)

Browser-only Trimble Connect 3D Viewer extension to preview selected road-surface objects at a specified vertical offset. No project geometry is permanently changed. Visual inspection only; no automatic clearance or clash calculation.

## Installation — separate repository

Repository: `https://github.com/jagkr1/road-clearance`

1. Upload `index.html` and `manifest.json` to the **root** of the `road-clearance` repository, commit to `main`. `README.md` is optional.
2. In GitHub, open **Settings → Pages**, select **Deploy from a branch**, branch **main**, folder **/(root)**, and save.
3. Wait for GitHub Pages to publish, then confirm both URLs load:
   - `https://jagkr1.github.io/road-clearance/`
   - `https://jagkr1.github.io/road-clearance/manifest.json`
4. In Trimble Connect for Browser, open the project's custom extensions/app settings and add the manifest URL: `https://jagkr1.github.io/road-clearance/manifest.json`.

## Usage

1. Load the road and tunnel/bridge models in the 3D viewer.
2. Select road-surface object(s) from **one model**.
3. Click **Use current 3D selection**.
4. Enter clearance in **centimetres** (for example, 450 cm = 4.50 m), then click **Show clearance surface**.
5. Inspect the temporary preview. Change height with **Update height**; remove it with **Remove preview**.

## Experimental limitations

- The extension relies on Trimble's temporary TrimBIM model API and may not work on all loaded source model types. The documented temporary blob size limit is 10 MB.
- Check that the preview contains **only** selected objects; if other objects are included, it is not a valid clearance display. Trimble's partial-visibility semantics can vary by viewer version and model structure.
- This is a vertical Z offset, not a guaranteed minimum clearance, dynamic vehicle envelope, or clash detector.
- If it fails, expand **Technical log** in the extension and share the messages so we can diagnose the issue.

## Changes in v0.3

- The previous version duplicated the entire road model at the offset height, with only selected objects recolored.
- Now the temporary copy is first loaded completely **hidden**, and then the extension calls the partial-visibility selector to show and color **only the selected road objects**.
- This is an API-based approach that needs testing in your actual Trimble Connect 3D Viewer. If other objects still appear elevated, do not treat the preview as a valid clearance surface; share the technical log and a screenshot.
- The original project model remains unchanged. This still does not perform automatic collision or minimum-clearance calculations.
- Updated the cache-busting query parameter in `manifest.json` to `?v=3`.

## Updating

When changing `index.html`, increment the cache-busting query in `manifest.json`, such as `?v=2` to `?v=3`, then commit both files.

Manifest registration/cache-busting URL: `https://jagkr1.github.io/road-clearance/manifest.json?v=3`
