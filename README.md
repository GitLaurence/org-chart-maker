# OrgChart Maker

A lightweight, single-file organizational chart builder built with vanilla HTML, CSS, and JavaScript. No frameworks, no dependencies, no server required.

## Features

- **Add people** with name, job title, department, reporting line, and color
- **Auto tree layout** — hierarchy repositions automatically on every change
- **Pan & zoom** — drag to pan, scroll to zoom, or use on-screen controls
- **Edit & delete** — inline action buttons or right-click context menu
- **Smart deletion** — direct reports are reassigned to the deleted person's parent
- **Auto-save** — chart persists in `localStorage` and restores on reload
- **Export / Import** — save and load charts as `.json` files

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
    "color": "#4f46e5"
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

`parentId` is `null` for top-level (root) nodes. Multiple root nodes are supported and displayed side by side.

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge).
