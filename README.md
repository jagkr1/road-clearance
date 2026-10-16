# Road Clearance Preview v0.7 — single-object visibility diagnostic

## Installation

Replace the root `index.html` and `manifest.json` in GitHub repository `jagkr1/road-clearance`; commit and ensure GitHub Pages has deployed the changes. Then open Trimble Connect using this capability manifest URL:

`https://jagkr1.github.io/road-clearance/manifest.json?v=7`

The manifest HTML URL should end in `index.html?v=7`.

## Test procedure

1. Select the road surface in the **original road model** and click **Use current 3D selection**.
2. Set an offset (e.g., 450 cm) and keep **Temporary copy ID (recommended, test B)** selected.
3. Click **Show clearance surface**. The current version will likely still duplicate the entire road model.
4. Select ONE unwanted object in the **elevated copy**, not the original model.
5. Click **Hide selected object in offset copy (test)**.
6. Report whether the chosen unwanted offset object actually disappears. If not, copy the new `v0.7 single-object HIDE` lines from Technical log.
7. Optionally click **Restore last test-hidden object**. Removing the preview removes the test copy.

The hide button explicitly verifies that the selected model ID matches the extension's current temporary copy. It does not make visibility changes to the source model. A resolved API call is *not* confirmation of successful hiding. No automatic clash or clearance calculation is performed.
