# 🎨 Texture Bake with Cage - Complete Usage Guide

## 🚀 Why This Add-On is Exciting & Different

### The Problem It Solves

Traditional texture baking in Blender is a **nightmare**:
- **Seam artifacts everywhere** - Ray casting from the surface creates inconsistent projections
- **Black texture bakes** - Imported GLB/OBJ meshes with unloaded textures result in completely black bakes
- **Manual cage setup** - Creating and managing bake cages is tedious and error-prone
- **No quality controls** - Aliasing, jagged edges, and pixelated seams are common
- **Complex workflows** - Requires dozens of manual steps across multiple editors

### What Makes This Different

🔥 **Automated Cage-Based Baking**
- Automatically generates perfectly-sized bake cages
- Adaptive inflation based on mesh bounding box (0.05%-2% of size)
- Eliminates seam lines completely - no more visible UV boundaries!
- Handles ray direction automatically - no manual ray distance tweaking

⚡ **Smart Quality Enhancements**
- **2× SSAA (Super-Sample Anti-Aliasing)** - Bakes at double resolution then downsamples for perfectly smooth edges
- **Smart Margin Scaling** - Automatically adjusts pixel bleed for high-resolution bakes
- **Auto EMIT Detection** - Automatically detects Emission shaders and switches bake mode (prevents dark textures)

🛠️ **Zero-Config Workflow**
- **One-Click Target Preparation** - Clears seams, unwraps UVs, creates materials, sets up 32-bit float textures
- **Smart UV Unwrapping** - Two methods: angle-based (organic) and seam-based (hard surface)
- **Material Transfer** - Optionally copies complete source material node trees to target

🔧 **Fixes Common Issues**
- **Black Bake Fix** - Automatically loads external textures from GLB/OBJ imports
- **Shader Conversion** - Temporarily converts Principled BSDF to Diffuse for accurate bakes, then restores
- **Image Loading** - Forces all texture images into GPU memory before baking
- **Normal Recalculation** - Ensures consistent outward-facing normals

📊 **Production-Ready Quality**
- 32-bit float image textures for HDR support
- Comprehensive error checking and warnings
- Detailed console logging for troubleshooting
- Preserves all source materials (doesn't modify originals)

---

## 📦 Installation

1. **Zip the add-on folder** (`uv_transfer_addon`)
2. **Install in Blender:**
   - `Edit` → `Preferences` → `Add-ons` → `Install...`
   - Select the zipped folder
3. **Enable the add-on:**
   - Search for "Texture Bake with Cage (4.5)"
   - Check the checkbox to enable
4. **Access the panel:**
   - Press `N` in the 3D Viewport (or `View` → `Sidebar`)
   - Click the **"Texture Bake"** tab in the sidebar

---

## 🎬 Quick Start (3 Steps)

### Step 1: Prepare Target (Low-Poly Mesh)

**Option A: Auto Prepare (Recommended for beginners)**
1. Select your **target** (low-poly) mesh
2. In the Texture Bake panel, click **"⚡ Auto Prepare (Recommended)"**
3. ✅ Done! UVs unwrapped, material created, texture ready

**Option B: Manual Preparation**
1. Select target mesh
2. Use **"Smart UV Project"** or **"Unwrap (Auto-Seams)"** for UV layout
3. Ensure material with Image Texture node exists

### Step 2: Configure Bake Settings

In the **"⚙ Step 2: Bake Settings"** section:

**Texture Resolution:**
- **Size**: `2048` (standard), `4096` (high-detail), `1024` (mobile)
- **Margin**: `16px` (default) - increase for tightly packed UVs

**Ray Casting:**
- **Max Distance**: `0.1` (default) - increase if source is far from target

**Cage Options:**
- ✅ **Use Cage (Recommended)**: Enable this! Eliminates seams
- **Inflation**: `0.01` (default) - automatically adjusted based on mesh size

**Quality Enhancements:**
- ✅ **2× SSAA**: Enable for smooth, anti-aliased textures (4× slower but much better)
- ✅ **Auto EMIT**: Automatically detects Emission shaders (prevents dark bakes)

**Material Transfer:**
- **Copy Source Materials**: Copy complete material node trees from source to target

### Step 3: Bake!

1. **Select SOURCE** (high-poly mesh) - Click to select
2. **Shift+Click TARGET** (low-poly mesh) - Add to selection
3. **Make TARGET active** - Click again (should be orange outline)
4. Click **"🔥 BAKE TEXTURE"**

⏱️ **Bake time:** 10 seconds - 5 minutes depending on resolution and quality settings

---

## 📖 Detailed Step-by-Step Workflow

### Workflow 1: Standard High-Poly → Low-Poly Bake

**Scenario:** You have a sculpted high-poly character and want to bake textures to a game-ready low-poly version.

1. **Import/Select Source Mesh**
   - High-poly sculpted mesh with materials and textures
   - Ensure textures are loaded (check Shader Editor)

2. **Prepare Target Mesh**
   - Select low-poly mesh
   - Click **"⚡ Auto Prepare"**
   - Or manually: Clear UVs → Smart UV Project → Create material

3. **Position Meshes**
   - Source and target should overlap (target inside source)
   - Both at world origin is recommended

4. **Configure Settings**
   - Size: `4096` for characters
   - Margin: `16-32px` depending on UV packing
   - ✅ Use Cage: **Enabled** (critical!)
   - ✅ Quality Mode: **Enabled** (for smooth results)
   - ✅ Auto EMIT: **Enabled**

5. **Bake**
   - Select SOURCE first
   - Shift+Select TARGET (make it active/orange)
   - Click **"🔥 BAKE TEXTURE"**

6. **Save Result**
   - Open Image Editor (`Shift+F10`)
   - Image named "UVT_Bake" should be visible
   - `Image` → `Save As...` → Choose location and format

### Workflow 2: Imported Model (GLB/OBJ) to Low-Poly

**Scenario:** You imported a model from another software and want to bake its textures.

1. **Import Source**
   - File → Import → GLB/OBJ
   - Check console for texture loading warnings
   - The add-on will attempt to auto-load textures

2. **Prepare Target**
   - Create or select low-poly version
   - Auto Prepare target mesh

3. **Verify Source Materials**
   - Click **"🔧 Show Mesh Info"** in Troubleshooting section
   - Check console for material issues
   - Fix any disconnected nodes if needed

4. **Bake with Quality**
   - Enable **2× SSAA** for imported textures (often need smoothing)
   - Enable **Auto EMIT** (some imported models use emission)
   - Click **"🔥 BAKE TEXTURE"**

### Workflow 3: Material Preservation

**Scenario:** You want to keep the source's complex shader setup on the target.

1. Follow standard workflow (Steps 1-4 above)
2. **Enable "Copy Source Materials"** checkbox
3. After baking:
   - Target gets complete source material node tree
   - Baked texture replaces image textures in copied materials
   - All shader nodes, connections, and settings preserved

---

## 🎛️ Settings Explained

### Texture Resolution

**Image Size**
- **256-512**: Mobile games, icons
- **1024**: Low-poly game assets
- **2048**: Standard (default) - good balance
- **4096**: High-detail characters, hero props
- **8192**: Maximum quality (very slow, large files)

**Margin (px)**
- Pixel bleed around UV islands
- **0-8px**: Minimal (risk of visible seams)
- **16px**: Default - safe for most cases
- **32-64px**: High-poly bakes, mipmaps, tightly packed UVs

### Ray Casting

**Max Ray Distance**
- How far rays can travel from target to source
- **0.01-0.1**: Close meshes (default 0.1)
- **0.1-1.0**: Meshes with gaps
- **1.0-10.0**: Very separated meshes (not recommended)

### Cage Options

**Use Cage (Recommended)**
- **✅ Enabled**: Creates invisible inflated cage - eliminates seams, fixes ray direction
- **❌ Disabled**: Uses ray extrusion (legacy method, seam artifacts)

**Cage Inflation**
- How much to expand cage outward
- **0.001-0.01**: Small meshes
- **0.01-0.05**: Medium meshes (default 0.01)
- **0.05-1.0**: Large meshes
- **Auto-adjusted** based on bounding box if cage enabled

### Quality Enhancements

**2× SSAA (Anti-Aliasing)**
- **Enabled**: Bakes at 2× resolution, downsamples (4× slower, dramatically better quality)
- **Disabled**: Standard bake (faster, may have aliasing)
- **Use when**: Character faces, smooth surfaces, high-quality renders

**Auto EMIT (Emission Detection)**
- **Enabled**: Auto-detects Emission shaders, switches bake mode
- **Disabled**: Always uses DIFFUSE mode
- **Use when**: Source has emission-based materials (glow, neon, etc.)

### Material Transfer

**Copy Source Materials**
- **Enabled**: Copies complete source material setup to target after baking
- **Disabled**: Creates simple Diffuse BSDF with baked texture
- **Use when**: Source has complex node trees you want to preserve

---

## 🛠️ Tools Reference

### Auto Prepare Target
**What it does:**
- Clears all UV seams
- Creates Smart UV unwrap
- Removes old materials
- Creates new Principled BSDF material
- Adds 32-bit float Image Texture (2048×2048 default)
- Sets texture as active for baking

**When to use:** Every time before baking to a new target

### Smart UV Project
**What it does:**
- Automatic angle-based UV projection
- No manual seam marking needed
- Fast and works for most meshes

**When to use:** Organic shapes, characters, complex geometry

### Unwrap (Auto-Seams)
**What it does:**
- Conformal unwrap with automatic seam detection
- Marks seams on sharp edges (~30° threshold)
- More predictable layout

**When to use:** Hard-surface models, mechanical objects, architecture

### Clear All UVs
**What it does:**
- Removes all UV coordinate layers
- Clean slate for re-unwrapping

**When to use:** Corrupted UV data, starting fresh

### Show Mesh Info
**What it does:**
- Displays UV layer count and names
- Shows material count and shader types
- Lists image textures
- Prints detailed info to console

**When to use:** Troubleshooting baking issues, verifying setup

---

## 🔧 Troubleshooting

### Problem: Black/Empty Texture After Baking

**Causes & Solutions:**

1. **Source textures not loaded** (imported GLB/OBJ)
   - ✅ **Solution**: Add-on auto-loads, but check console warnings
   - Check Image Editor for loaded textures
   - Manually load: Shader Editor → Image Texture → Open

2. **Material not connected properly**
   - ✅ **Solution**: Use "Show Mesh Info" to check connections
   - Verify: Image Texture → BSDF → Material Output
   - Fix disconnected nodes in Shader Editor

3. **Source too far from target**
   - ✅ **Solution**: Increase "Max Ray Distance" setting
   - Or move meshes closer together

4. **Principled BSDF issues**
   - ✅ **Solution**: Add-on auto-converts to Diffuse during bake
   - Should work automatically, but check console for warnings

### Problem: Visible Seam Lines

**Causes & Solutions:**

1. **Cage disabled**
   - ✅ **Solution**: Enable "Use Cage (Recommended)"

2. **Cage inflation too small**
   - ✅ **Solution**: Increase "Cage Inflation" value
   - Or let auto-sizing handle it (default)

3. **UV margin too small**
   - ✅ **Solution**: Increase "Margin (px)" to 24-32px

### Problem: Aliasing/Jagged Edges

**Causes & Solutions:**

1. **Quality Mode disabled**
   - ✅ **Solution**: Enable "2× SSAA (Anti-Aliasing)"

2. **Resolution too low**
   - ✅ **Solution**: Increase "Image Size" to 4096 or higher

### Problem: Bake Takes Forever

**Causes & Solutions:**

1. **Quality Mode + High Resolution**
   - ✅ **Solution**: Disable 2× SSAA or reduce size
   - Quality Mode = 4× bake time

2. **Very high resolution**
   - ✅ **Solution**: Use 2048 instead of 8192 for testing

### Problem: Wrong Colors (Too Dark/Bright)

**Causes & Solutions:**

1. **Emission shader not detected**
   - ✅ **Solution**: Enable "Auto EMIT" (should be on by default)

2. **Color space issues**
   - ✅ **Solution**: Check Image Texture color space in Shader Editor
   - Albedo should be "sRGB", Normal maps "Non-Color"

### Problem: Source Mesh Modified After Bake

**Note:** Source mesh is **never modified**. If you see changes:
- Check if you accidentally selected wrong object
- Verify source materials are restored (check console messages)
- Add-on automatically restores all source shaders after baking

---

## 💡 Tips & Best Practices

✅ **Always use Auto Prepare** for new targets - ensures clean setup

✅ **Enable Quality Mode** for final bakes - dramatically better results

✅ **Keep Cage enabled** - it's the core feature that eliminates seams

✅ **Start with 2048** resolution - test workflow, then increase if needed

✅ **Check console output** - detailed logging helps debug issues

✅ **Save before baking** - large meshes can take time

✅ **Position meshes close** - target should be inside/overlapping source

✅ **Use Auto EMIT** - prevents dark textures from emission materials

✅ **Copy Source Materials** only if you need complex node trees

✅ **32-bit float textures** - enabled by default for HDR support

---

## 🎯 Common Workflows Summary

| Workflow | Target Prep | Size | Quality | Cage | Auto EMIT | Copy Materials |
|----------|-------------|------|---------|------|-----------|----------------|
| **Game Asset** | Auto | 2048 | ✅ | ✅ | ✅ | ❌ |
| **Character** | Auto | 4096 | ✅ | ✅ | ✅ | ❌ |
| **High-Quality Render** | Auto | 4096 | ✅ | ✅ | ✅ | ✅ |
| **Quick Test** | Auto | 1024 | ❌ | ✅ | ✅ | ❌ |
| **Mobile/VR** | Auto | 1024 | ❌ | ✅ | ✅ | ❌ |

---

## 📝 Technical Notes

### Bake Process Flow

1. **Image Loading** - Forces all source textures into GPU memory
2. **Material Verification** - Checks shader connections
3. **Shader Conversion** - Temporary Principled → Diffuse conversion
4. **Cage Creation** - Adaptive inflation based on bounding box
5. **Bake Execution** - Cycles render with cage-based ray casting
6. **Downsampling** - 2× SSAA downscale if enabled
7. **Material Transfer** - Copies source materials if requested
8. **Shader Restoration** - Converts source back to original shaders

### Image Formats

- **Internal**: 32-bit float (HDR support)
- **Export**: PNG (lossless), EXR (HDR), TGA, JPEG (lossy)

### Performance

- **Standard Bake**: ~10-60 seconds (2048, no SSAA)
- **Quality Mode**: ~40-240 seconds (2048 with 2× SSAA)
- **High-Resolution**: ~60-600 seconds (4096+)

---

## 🎬 That's It!

You now have professional-grade texture baking in Blender with:
- ✅ Zero-seam artifacts
- ✅ Automated workflow
- ✅ Quality enhancements
- ✅ Production-ready results

**Happy Baking!** 🎨🔥

