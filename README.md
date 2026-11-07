# Stereo 4D polytopes

**[Live demo](https://well-made.github.io/4d-polytope-viewer/)**

An interactive, single-file viewer for 4D polytopes (**tesseract** and **5-cell**) shown as stereo pairs, so you can *see* their depth with the naked eye, rotate them in all six 4D rotation planes, and optionally add a "wiggle" as a second depth cue.

No libraries, no build step, no network access: open `index.html` in a browser, or serve the folder with GitHub Pages.

> Assumed background: you know roughly what a tesseract is and how stereo pairs work. Everything else is explained below.

## Quick start

1. Open `index.html` (double-click, or enable **GitHub Pages**: *Settings → Pages → Deploy from branch → `main` / root*).
2. Drag with the left mouse button to rotate. Drag with the **right** button to rotate "through the fourth dimension".
3. Look at the two images of a pair so that they fuse into one 3D picture (see the next section). Or just switch the wiggle on and enjoy the motion parallax - no stereo skill needed.

## How to view the stereo pair

The page shows **two stereo pairs** (top and bottom), each made of a left and a right image.

| Method | What to do | Setting |
|---|---|---|
| **Parallel** (default) | Relax your eyes as if looking *through* the screen at something far away, until the two images drift together and fuse into a third, central one. The left eye must end up seeing the left image. | *Stereo pair → Viewing method → Parallel* |
| **Cross-eyed** | Cross your eyes slightly until the two images overlap. The left eye then sees the right image. | *Cross-eyed* |

Tips: if it is hard to fuse, reduce *Image spacing* (for parallel viewing the centres of the two images should not be farther apart than your eyes, i.e. about 6-7 cm on the screen) or reduce *Stereo strength*.

## What the two pairs are

Both pairs show the same figure, but the two "depth cues" - the left/right difference (**stereo**) and the camera oscillation (**wiggle**) - are applied in different places:

| | Stereo (left/right difference) | Wiggle (camera oscillation) |
|---|---|---|
| **Variant 1** (top) | in the 3D view: you see ordinary 3D depth | in the 4D step: the 4th dimension reveals itself by motion |
| **Variant 2** (bottom) | in the 4D step: depth along **W** appears as stereo depth | in the 3D view: ordinary 3D depth by motion |

The captions above each pair say which is which (the wiggle part is hidden while the wiggle is off).

## Controls

### Mouse and touch

| Action | Effect |
|---|---|
| Left drag | Rotate in the **XZ** (horizontal) and **YZ** (vertical) planes - an ordinary 3D rotation |
| Right drag | Rotate in the **XW** (horizontal) and **YW** (vertical) planes - rotation through the 4th dimension |
| Right button + wheel | Rotate in the **ZW** plane (10° per wheel notch) |
| Left + right together, drag left/right | Rotate in the **XY** plane (roll in the screen plane). You can press or release the second button in the middle of a drag |
| Wheel / two-finger pinch | Zoom |
| Touch, one finger | Same as left drag (there is no 4D rotation on touch screens) |

Rotations are applied in the **fixed screen frame** (X right, Y up, Z toward you, W toward the 4D observer), so dragging always feels the same, whatever the current orientation is.

### Panel

| Control | What it does |
|---|---|
| **Tesseract / Simplex** | Switch the figure. Orientation, zoom and sliders are kept; each figure remembers its own highlighted cells |
| **Reset orientation** | Return to the initial orientation (zoom and sliders stay) |
| **Edges: W gradient / Plain** | Colour edges by 4D depth (see below), or draw them in one colour |
| **Cell toggles** | Highlight cells with a semi-transparent fill. Each button is an independent on/off switch. Tesseract: one row per axis with a **−** and a **+** button (both on = the whole pair of opposite cubes). 5-cell: five buttons, one per cell |
| **Fill opacity** | Opacity of the highlighted cells |
| **Wiggle** (checkbox) | Switch the camera oscillation on/off |
| **Wiggle direction** | Oscillate horizontally or vertically |
| **Motion: Smooth / Step** | Sine-wave motion or a two-position flip |
| **Amplitude / Frequency** | Size of the oscillation and its speed (Hz) |
| **3D field of view** | Perspective strength of the 3D → 2D step. A larger angle means stronger perspective |
| **4D field of view (along W)** | Perspective strength of the 4D → 3D step |
| **Viewing method** | Parallel or cross-eyed (swaps the left and right camera) |
| **Image spacing** | Horizontal distance between the left and right image of a pair |
| **Pair spacing** | Vertical distance between the top and the bottom pair |
| **Stereo strength** | How far apart the two virtual eyes are (bigger = stronger depth effect) |

## Visual cues

* **Edge colour** (*W gradient* mode): the colour shows how far a point is along the 4th dimension *after the current rotation*. **Blue** = far from the 4D observer (small W), **red** = near (large W). An edge fades from the colour of one end to the colour of the other. This is the main clue for telling "inner" parts of the figure from "outer" ones, e.g. the small inner cube of a tesseract versus its big outer cube.
* **Coloured axes in the lower-left corner of each image**: the *fixed* global axes of the screen frame. They do **not** rotate with the figure - they show the directions you are rotating relative to.
  * **+X** (red) right, **+Y** (green) up, **+Z** (blue) toward you, **+W** (gray) toward the 4D observer.
  * Z and W both point "into the screen", so they look nearly collinear; their labels are shifted apart. They are projected like the figure, so the field-of-view sliders change their length.
  * In variant 1 the **W** axis moves with the wiggle while **Z** only shows the stereo shift; in variant 2 it is the other way round (**Z** wiggles, **W** shows the stereo shift). X, Y and the origin never move. While the wiggle is off, the axis that exists to show it (W in variant 1, Z in variant 2) is not drawn.
* **Highlighted cells**: filled with a semi-transparent colour.
  * Tesseract: a cell takes the colour of its axis - X red, Y green, Z blue, W gray; "−" and "+" mean the cell at the negative or positive end of that axis. By default the W− cell (the inner cube at the start orientation) is on.
  * 5-cell: cells are numbered 1-5 (colours red, green, blue, gray, orange). **Cell k is made of all vertices except vertex k.** Vertex 5 is the apex, pointing along +W at the start orientation; cell 5 is therefore the opposite "base" tetrahedron.
* **Captions** above the pairs: which variant it is, and (while the wiggle is on) which space wiggles.

## The figures

| | Vertices | Edges | Faces | Cells | Note |
|---|---|---|---|---|---|
| Tesseract (8-cell) | 16 | 32 | 24 squares | 8 cubes | vertices at (±100, ±100, ±100, ±100) |
| Simplex (5-cell) | 5 | 10 | 10 triangles | 5 tetrahedra | 4 vertices form a regular tetrahedron, the 5th is the apex on +W; all edges are equal |

## How it works (short version)

1. **Orientation.** The figure's orientation is a 4×4 rotation matrix. Dragging multiplies it by a small rotation in one of the six coordinate planes (XY, XZ, XW, YZ, YW, ZW); the matrix is re-orthonormalised each time so rounding errors never accumulate.
2. **Projection.** A 4D point goes through two perspective steps: **4D → 3D** (a camera on the W axis; points with larger W look larger and move outward) and then **3D → 2D** (a camera on the Z axis, the usual perspective). The two *field of view* sliders set the strength of each step.
3. **Stereo.** Each image of a pair is rendered by a camera shifted sideways by ± *Stereo strength*. Shifting the camera moves a point sideways by an amount that depends on its depth, which creates the left/right difference your brain turns into depth. In *variant 1* the shift is applied in the 3D → 2D step, in *variant 2* in the 4D → 3D step.
4. **Wiggle.** The same camera offset, but equal for both eyes and oscillating in time. Depth is then perceived from motion parallax. It is applied to the step that does *not* carry the stereo shift.
5. **Cell highlight.** A shape stores its cells as lists of faces; highlighted faces are filled before the edges are drawn.
6. **Global axes.** A small frame in the same 4D space, not affected by the rotation, positioned in the plane `z = 0, w = 0` so that each axis reacts only to the camera shift that belongs to it.

## Code map and adding a figure

Everything is in `index.html` (the code is commented for both people and AI assistants; sections are numbered `SECTION 1…10`):

| Section | Content |
|---|---|
| 1-2 | DOM references, colours |
| 3 | **Shapes** - plain data objects (vertices, edges, cells as lists of faces) |
| 4-5 | State, 4D rotation maths |
| 6 | Rendering: projection, cell fill, edges, global axes, captions |
| 7 | Mouse and touch input |
| 8 | Wiggle loop and button groups |
| 9 | Cell highlight panel |
| 10 | Figure switch, reset, start-up |

To add another regular polytope (16-cell, 24-cell, …), write one `makeXxx()` function in SECTION 3 that returns `{ id, V, E, cells, colors, on }` (see the comment there), register it in `SHAPES`, and add a button with `data-v="<id>"` inside `#segShape`. If it needs its own cell-toggle panel, extend `buildCellUI()` in SECTION 9. The renderer does not need to change. For polytopes with hundreds of edges you may want to cache the per-edge gradients, since a frame draws every edge four times.

## Limitations

* No 4D rotation on touch screens (one finger acts like the left mouse button).
* Rendering uses the 2D canvas and draws each edge with its own gradient, which is comfortable for small figures but not meant for polytopes with hundreds of edges.
