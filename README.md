# Road Clearance Preview v0.10 — bounding-box verified IDs (experimental)

Upload `index.html` and `manifest.json` into the root of the existing `jagkr1/road-clearance` GitHub repository.

Trimble Connect manifest URL: `https://jagkr1.github.io/road-clearance/manifest.json?v=10`

## Why v0.9 failed
The `getObjects()` scan appeared to return every speculative runtime ID from 0 through 8191. That does **not** establish that the model has that many geometry objects. The previous scanner could not distinguish returned placeholders from valid geometry IDs. It stopped at a safety limit and removed the preview.

## What v0.10 changes

- Creates a temporary TrimBIM copy as before.
- Queries `getObjectBoundingBoxes()` on the **original model** for the selected runtime ID(s) and a deliberately nonexistent sentinel ID. If the result fails validation, it stops without hiding anything.
- Scans bounded ranges of runtime IDs, accepting only those with real, finite bounding boxes; never treats a mere ID echo as proof of geometry.
- Excludes selected IDs plus known hierarchy ancestors/descendants from the hide list.
- Sends `setObjectState` hide requests only to the **temporary copy's model ID**; does not modify the original model.
- Removes the temporary copy if the probe fails, no unselected geometry is found or the bounded scan cannot be completed reliably.

**Limitations:** Some model types may not return bounding boxes for surfaces. A valid-box-only scan can miss objects that have no bounding box or IDs outside the scanned region. This is a visualization prototype, not a guaranteed isolation, clash check, or minimum-clearance certification. Visually verify that no unwanted elevated geometry remains.

## Test

1. Confirm the technical log says `v0.10`.
2. Select road surface, capture selection and enter 450 cm.
3. Click Show clearance surface.
4. If only the raised surface remains, report success. If the preview disappears, send the log including `bbox probe`.
