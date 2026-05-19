# OrgChart Maker

A lightweight, single-file organizational chart builder built with vanilla HTML, CSS, and JavaScript. No frameworks, no dependencies, no server required.

## Features

- **Add people** with name, job title, department, reporting line, and color
- **Photo avatars** — upload an image or extract a photo from a PDF for each person
- **Auto tree layout** — hierarchy repositions automatically on every change
- **Pan & zoom** — drag to pan, scroll to zoom, or use on-screen controls
- **Edit & delete** — inline action buttons or right-click context menu
- **Smart deletion** — direct reports are reassigned to the deleted person's parent
- **Auto-save** — chart persists in `localStorage` and restores on reload
- **Export / Import** — save and load charts as `.json` files (photos included)

## Usage

Open `index.html` in any modern browser. No build step or server needed.

```
double-click index.html
```

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `+` / `=` | Zoom in |
| `-` | Zoom out |
| `0` | Fit chart to screen |
| `Enter` | Save the open form |
| `Esc` | Close modal / menu |

## Mouse Controls

| Action | Gesture |
|--------|---------|
| Pan | Click and drag on the canvas background |
| Zoom | Scroll wheel |
| Context menu | Right-click any card |

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

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge).
