# OrgChart Maker

A lightweight, single-file organizational chart builder built with vanilla HTML, CSS, and JavaScript. No frameworks, no dependencies, no server required.

## Features

- **Add people** with name, job title, department, reporting line, and color
- **Photo avatars** — upload an image or extract a photo from a PDF for each person
- **Layout presets** — switch between Top→Down, Left→Right, and Compact layouts from the header
- **Draggable cards** — unlock cards to freely reposition any node; manual positions are saved
- **Auto tree layout** — hierarchy repositions automatically when switching presets or adding people
- **Pan & zoom** — drag to pan, scroll to zoom, or use on-screen controls; pinch-to-zoom on touch
- **Mobile responsive** — automatically stacks cards vertically on small screens; layout picker opens as a bottom sheet
- **Edit, duplicate & delete** — inline action buttons or right-click / long-press context menu; duplicate quickly clones a person (name, title, department, color, photo) as a sibling
- **Smart deletion** — direct reports are reassigned to the deleted person's parent
- **Undo** — deleting a person or clearing the chart shows an Undo action for a few seconds
- **Search** — find people by name, title, or department; matches are highlighted and the chart pans to the first result
- **Auto-save** — chart, layout preference, and card positions persist in `localStorage` and restore on reload
- **Export / Import** — save and load charts as `.json` files (photos included); malformed entries, invalid photo data, and broken/cyclic reporting lines are sanitized on import. Imported files always get freshly generated internal IDs, so a crafted `.json` can't inject markup or script into the chart.
- **Export as Image** — download a PNG snapshot of the entire chart (not just the visible viewport) via the Export menu

## Usage

Open `index.html` in any modern browser. No build step or server needed.

```
double-click index.html
```

## Layout Presets

Click the **Layout** button in the header to choose how the hierarchy is displayed:

| Preset | Description |
|--------|-------------|
| Top → Down | Classic tree — root at top, children spread horizontally below (default) |
| Left → Right | Root on the left, children stack vertically to the right — great for deep hierarchies |
| Compact | Same top-down algorithm with smaller cards and tighter spacing — more nodes visible at once |

Switching presets resets any manually dragged positions and re-fits the chart to the screen. Your chosen preset is remembered across page reloads.

On mobile (≤ 640 px), all presets use a vertical single-column stack regardless of selection.

## Draggable Cards

Click the **Lock** button in the header to toggle card dragging:

- **Locked** (default) — cards are fixed; pan and zoom work normally; no accidental moves
- **Unlocked** — each card shows a grab cursor; drag any card to reposition it; connector lines redraw live

Manually placed positions are saved per-node and survive page reloads. Switching to a different layout preset clears all manual positions and returns to the algorithm layout.

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `+` / `=` | Zoom in |
| `-` | Zoom out |
| `0` | Fit chart to screen |
| `Enter` | Save the open form |
| `Esc` | Close modal / menu / search |
| `/` | Open search |

## Mouse & Touch Controls

| Action | Gesture |
|--------|---------|
| Pan | Click and drag on the canvas background |
| Zoom | Scroll wheel |
| Fit view | Click the **Fit** button in the header |
| Context menu | Right-click any card |
| Context menu (touch) | Long-press any card |
| Pinch zoom | Two-finger pinch on touch screens |

## Photo Avatars

Each person can have a photo avatar instead of the default colored initials circle.

**Upload Image** — click "Upload Image" in the edit form to pick any image file (JPEG, PNG, WebP, etc.). It is automatically cropped to a square and compressed to ~96×96 px JPEG.

**Pick from PDF** — click "Pick from PDF" to open a company directory or any PDF. Navigate through pages, then drag a rectangle over the headshot you want. Click **Use Selection** to crop and assign it as the avatar.

Photos are stored as base64 strings inside each person's data and travel with Export/Import JSON. Each photo is roughly 3–5 KB; 50 people with photos ≈ 150–250 KB total.

> **Note:** PDF support requires an internet connection on first load to fetch the PDF.js library from unpkg.com.

## Data Format

Charts are saved as a JSON array. Each person is an object:

```json
[
  {
    "id": "abc123",
    "name": "Jane Smith",
    "title": "CEO",
    "dept": "Executive",
    "parentId": null,
    "color": "#4f46e5",
    "photo": "data:image/jpeg;base64,..."
  },
  {
    "id": "def456",
    "name": "John Doe",
    "title": "CTO",
    "dept": "Engineering",
    "parentId": "abc123",
    "color": "#0891b2"
  }
]
```

`parentId` is `null` for top-level (root) nodes. Multiple root nodes are supported and displayed side by side. `photo` is optional — omit it or set it to `null` to use the default initials avatar.

## localStorage Keys

| Key | Contents |
|-----|----------|
| `orgchart_v1` | Node data (JSON array) |
| `orgchart_prefs_v1` | Active layout preset and lock state |
| `orgchart_positions_v1` | Manually dragged card positions |

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge).
