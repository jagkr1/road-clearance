# Road Clearance Preview v0.8 — automated visibility filtering (experimental)

## Installation

Replace `index.html` and `manifest.json` in the root of **jagkr1/road-clearance**. Commit, and wait for GitHub Pages deployment. Use the Trimble Connect capability URL:

`https://jagkr1.github.io/road-clearance/manifest.json?v=8`

Confirm the technical log says `connected (v0.8)` before testing.

## What changed

- v0.7 demonstrated that `setObjectState` with `visible:false` can hide a manually selected individual object in a temporary copy.
- v0.5 could **not** enumerate a temporary copy through `getObjects`.
- v0.8 gets the object IDs from the original road model **read-only**, creates the temporary copy, then explicitly hides all unselected IDs in the **temporary copy**. It protects the selected objects and their hierarchy relations where the hierarchy API is available.
- Moving the preview reapplies the object-hiding mask.
- On failure, the temporary model is removed.

## Test

1. Select one road surface in the original model and click **Use current 3D selection**.
2. Keep height at **450 cm** and click **Show clearance surface**.
3. **Visually verify** that ONLY the selected road surface is raised and other objects remain in their original locations.
4. If the viewer reports `Source-model enumeration returned zero objects`, send the full Technical log: this is a new, distinct API limitation; the extension will not create a misleading full copy.
5. If extra elevated objects remain visible, send the log and indicate whether an unwanted object still responds to the optional single-object hide test.

This extension is a **visual aid only**, not a certified clearance analysis. It makes no permanent changes to the original model or properties. The selected model and the temporary copy are different IDs, and visibility changes are directed only at the temporary model.
