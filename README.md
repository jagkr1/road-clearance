# Road Clearance Preview v0.5 — explicitly hide unwanted objects

Deploy these two root-level files to the existing `jagkr1/road-clearance` GitHub repository: `index.html`, `manifest.json`.

**Manifest URL in Trimble Connect:** `https://jagkr1.github.io/road-clearance/manifest.json?v=5`

## What changed since v0.4

- Creates the temporary, elevated TrimBIM copy **visible from the start**.
- Enumerates its runtime object IDs through `viewer.getObjects`.
- Explicitly hides only IDs not in the selected road-object list using `viewer.setObjectState` in batches. This avoids the ambiguous "hide every object in the model" call.
- Reveals and recolors the selected objects last; does not issue a full-model visible toggle afterwards.
- Checks visibility when possible; removes the temporary copy if the API confirms unwanted geometry is visible. A 0-object result is treated as inconclusive, rather than success.
- Adds a diagnostic button **Log currently selected object IDs**. If the copy still shows unwanted surfaces, click one of those surfaces, click this button, and send the resulting log. This tells us which runtime model ID the viewer actually selects.

**Caveats:** This version is an API compatibility experiment, not proven in Trimble Connect for Browser. Do not rely on its visual clearance result unless the original remains unchanged and **only the selected objects** are offset. It does not calculate clashes or clearance compliance. Temporary copies are removed via `removeTrimbimModel`, not saved to the project.
