# Road Clearance Preview v0.4 — diagnostic visibility test

**Repository:** https://github.com/jagkr1/road-clearance

## Deploy
1. Replace root-level `index.html` and `manifest.json` in the existing `road-clearance` GitHub repository; commit to `main`.
2. Confirm GitHub Pages is published.
3. Refresh Trimble Connect, using the versioned manifest URL:
   `https://jagkr1.github.io/road-clearance/manifest.json?v=4`

## Test
1. Select one or more road-surface objects, all belonging to the same original model.
2. In the extension, click **Use current 3D selection**.
3. Set a height (for example 450 cm) and click **Show clearance surface**.
4. Check the offset copy visually and open **Technical log**. If the viewer refuses object-level visibility, it should clean up the incorrect preview and log a diagnostic.

## What changed
- v0.3 tried to hide the entire temporary model and then reveal a subset using `addTrimbimModel({visible:true, selector:...})`. In practice the entire offset copy remained visible.
- v0.4 instead attempts to use `viewer.setObjectState` on the **unique temporary model ID** (hide all objects, then reveal and recolor selected runtime IDs).
- Before doing that, it queries `viewer.getObjects` to check that temporary objects are addressable by their own model ID. If not, it does **not** try to modify the original model and removes the temporary copy.
- After the visibility changes, it checks `getObjects` visibility counts and removes obviously unfiltered previews. This is an experimental host compatibility test, not proof of geometric validity or of minimum clearance.

## Limitations
- If Trimble does not expose temporary TrimBIM objects through `getObjects` and `setObjectState`, this approach will not work. An alternative would require a standalone selected-geometry TrimBIM extract, which the current simple Workspace API does not directly provide.
- The model is not permanently changed. This is visual only; it does not calculate intersections, vehicle envelopes or guaranteed minimum clearances.
- If an error appears, copy the **Technical log** into the conversation.
