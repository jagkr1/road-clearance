# Road Clearance Preview v0.9 — explicit-ID scan (experimental)

## Installation

Upload `index.html` and `manifest.json` to the root of `jagkr1/road-clearance`. Set the Trimble Connect manifest URL to:

`https://jagkr1.github.io/road-clearance/manifest.json?v=9`

Check the technical log for `(v0.9)` before testing.

## Reason for this version

V0.8 queried `getObjects` using only the source model ID; it returned a model group with zero objects. V0.4 proved that `getObjects` can retrieve objects in a temporary model using **explicit runtime IDs**.

V0.9 creates the temporary copy, confirms it can retrieve the selected object(s) by ID, scans explicit runtime ID ranges in batches of 128, and hides unselected IDs **in the temporary copy only** with the successful v0.7 `setObjectState(..., {visible:false})` call. It protects selected objects, plus any available hierarchy ancestors/descendants.

For performance, scanning stops after at least 1024 IDs and four consecutive empty 128-ID batches, or fails at the 8192-ID safety limit. These are heuristics: **the scan is not exhaustive**, so users must visually verify the elevated copy contains ONLY the selected surface. Any failure during scanning removes the temporary model and does not modify original visibility.

## Testing

1. Select road object 43 (or another road surface) and capture selection.
2. Set 450 cm and click Show clearance surface.
3. Verify original model is unchanged and only selected geometry appears elevated.
4. If an error appears or extra geometry is raised, send the technical log; we need scan counts and highest returned runtime ID.

The preview is not a geometric clash measurement or certified height check.
