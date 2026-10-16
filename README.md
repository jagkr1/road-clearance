# Road Clearance Preview v0.6 — selector-at-load diagnostic

**Experimental; not a clearance verification or clash test.**

Version v0.5 could not enumerate temporary TrimBIM objects using `viewer.getObjects()`.
Version v0.6 therefore avoids `getObjects()`/`setObjectState()` on the copy and sends Trimble's documented `TrimbimModel.selector` in the **initial** `addTrimbimModel()` call.

## Deployment
- Replace repository-root `index.html` and `manifest.json` in `jagkr1/road-clearance`.
- Commit and wait for GitHub Pages.
- Re-register manifest `https://jagkr1.github.io/road-clearance/manifest.json?v=6`.
- Confirm log starts `v0.6`.

## Test
1. Select only one road object in the original model, click **Use current 3D selection**.
2. Enter 450 cm. Keep **Source model ID (test A)**, click **Show clearance surface**.
3. Verify visually whether only selected geometry is elevated. Remove the preview before the next test.
4. If the entire model is raised, choose **Temporary copy ID (test B)** and repeat.
5. Send Technical log AND tell us which test displays only selected geometry, if either.

This is a visibility experiment. It doesn't compute the actual minimum distance to a tunnel roof. The temporary preview is removed through `removeTrimbimModel()` and does not change the original model's visibility or placement.
