# Road Clearance Preview v0.11 — direct 3D selection

Upload `index.html` and `manifest.json` to the **root** of your existing `jagkr1/road-clearance` GitHub repository, replacing the current files.

Trimble Connect manifest URL:
`https://jagkr1.github.io/road-clearance/manifest.json?v=11`

## Change from v0.10

- Removed **Use current 3D selection**. After selecting a road surface in the viewer, click **Show clearance surface** directly.
- **Show clearance surface** reads the *current* viewer selection at click time, so it cannot use an outdated previously captured selection.
- Shows a clear error when nothing is selected, when objects come from several source models, or when the selected object belongs to an existing offset preview.
- **Update height** and **Remove preview** behave as before.
- The tested v0.10 bounding-box inventory, original-model hierarchy protection, and temporary-copy object hiding logic are unchanged.

## Test

1. Confirm the technical log says `v0.11`.
2. Select the road surface in the original model.
3. Enter a clearance height such as 450 cm and click **Show clearance surface**. There is no confirmation button.
4. Verify that only the selected surface appears raised, while the original road model stays unchanged.
5. Optionally change the height using **Update height** and then remove the preview.

**Limitation:** The bounded runtime-ID scan can miss unusually sparse geometry IDs or geometry without bounding boxes. This preview is a visual design aid, not a certified clearance measurement. Visually inspect the result.
