UV Transfer + Bake + GN Debug (4.5)
===================================

What's new
----------
- Quality Mode (2× SSAA): reduces aliasing & seam halos by baking at 2x and downsampling.
- Auto EMIT: if the source material output is emission-driven, bake with EMIT; otherwise uses DIFFUSE(Color only).
- Adaptive cage inflation and smart margin for cleaner transfers.

Install / Update
----------------
1) Zip this folder and install in Blender: Edit → Preferences → Add-ons → Install...
2) Enable "UV Transfer + Bake + GN Debug (4.5)".
3) In the "UV Transfer" sidebar tab:
   - Set Source object, select Target (active).
   - Use "Transfer UVs (DataTransfer)" for clean UV copy.
   - Use "Selected→Active Texture Bake" with optional Quality Mode / Auto EMIT.
