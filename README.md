# BrainMap

**A mind-mapping canvas for people who study by connecting things.** Nodes hold Markdown, groups nest inside each other, and cross-cutting themes link ideas that sit far apart on the canvas. Runs entirely in your browser, no account, no server.

[![Live demo](https://img.shields.io/website?url=https%3A%2F%2Fmap.schndrdavid.eu&label=live&up_message=online&down_message=offline&style=flat-square)](https://map.schndrdavid.eu/)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![No build step](https://img.shields.io/badge/build-none-brightgreen?style=flat-square)](#running-it-locally)

**➡️ [map.schndrdavid.eu](https://map.schndrdavid.eu/)**

<!-- Add a screenshot here: save it to docs/screenshot.png -->
<!-- ![Screenshot](docs/screenshot.png) -->

---

## Why it exists

Most mind-mapping tools force a strict tree: one parent, many children. Real study material is messier than that. A single concept belongs to one chapter but relates to three others, and the connections that matter for an exam are exactly the ones a tree can't express.

BrainMap keeps the free-form canvas but adds two things on top: **nested groups** for structure and **themes** for the connections that cut across that structure. Everything else follows from there.

## Features

### Canvas

- Free placement, pan and zoom, multi-select with a drag box
- Connect nodes by dragging from a node's anchor point onto another node
- Automatic layout via a d3 force simulation when hand-arranging gets tedious
- Minimap for orientation on large maps
- Multiple maps as tabs — reorderable by dragging, colour-codeable, renameable

### Nodes

- **Markdown content** with a live preview tab, rendered by `marked`
- **Seven statuses** with distinct colours, so you can see at a glance what's an open question, what's answered, and what still needs review
- **Tags** and full-text search across titles, content, and tags
- **Images** — drop an image file anywhere on the canvas and it becomes a node
- Collapsible preview so dense nodes stay readable

### Structure

- **Nested groups** — groups can contain other groups, and filtering by a parent group includes everything below it. Rendered as a coloured region behind the nodes.
- **Themes** — a colour-coded label you can attach to any number of nodes regardless of where they sit or which group they belong to. Click a theme's dot and every node carrying it lights up across the whole map. This is what a tree structure can't do.
- Filter the canvas by status, group, or search term

### Safety and output

- **Undo / redo**, 50 steps deep, per map
- **Automatic local backups** every 10 minutes, last 5 kept, restorable from a dialog
- **JSON export / import** of everything, or import a single map alongside your existing ones
- **PNG export** of the whole map, framed and scaled automatically
- **Print to A3 landscape** with the UI chrome stripped out
- **Light and dark theme**

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| <kbd>N</kbd> | new node |
| Double-click canvas | new node at that spot |
| <kbd>Delete</kbd> / <kbd>Backspace</kbd> | delete selected nodes |
| <kbd>Ctrl</kbd>+<kbd>Z</kbd> | undo |
| <kbd>Ctrl</kbd>+<kbd>Y</kbd> / <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Z</kbd> | redo |
| <kbd>Ctrl</kbd>+<kbd>A</kbd> | select all |
| <kbd>Ctrl</kbd>+<kbd>P</kbd> | print the map |
| <kbd>0</kbd> | reset viewport |
| <kbd>Esc</kbd> | clear selection and highlights |
| <kbd>Shift</kbd> / <kbd>Ctrl</kbd> + drag | drag a selection box |
| Drag empty canvas | pan |
| Scroll wheel | zoom toward the cursor |

## Where your data lives

Everything is stored in the browser's `localStorage` under `mindmap-statnice-v2`, with rolling backups under `mindmap-statnice-backups-v1`. Nothing is sent anywhere — there is no backend and no analytics.

Two practical consequences:

- Your maps are tied to one browser on one domain. Clearing site data wipes them. Use **Export** for real backups and for moving between machines.
- `localStorage` caps out somewhere around 5–10 MB depending on the browser. Dropped images are stored inline as base64, so a map heavy on images will hit that ceiling long before one that's mostly text. Individual images are capped at roughly 600 KB, and the app warns you when a save fails.

## Running it locally

No build, nothing to install:

```bash
git clone https://github.com/SchndrDavid/brainmap.git
cd brainmap
python3 -m http.server 8000
```

Open `http://localhost:8000`. Opening `index.html` directly works too, but `file://` gives each path its own separate `localStorage`, so use a server or the live version for real work.

## Built with

| | |
| --- | --- |
| UI | React 18.3.1 (UMD build) |
| Transpilation | Babel Standalone, in the browser |
| Layout engine | d3-force 7.9.0 |
| Markdown | marked 12.0.2 |
| PNG export | html2canvas 1.4.1 |
| Storage | `localStorage` |
| Hosting | GitHub Pages, static deploy from `main` |

All dependencies are loaded from cdnjs at exact pinned versions. The whole app is deliberately **a single file with no build step** — clone it, open it, it runs. The trade-off is that Babel compiles the JSX in the browser, which costs a moment on first load.

## Known limitations

- Storage ceiling as described above; image-heavy maps will hit it
- Node positions are absolute, so there is no automatic reflow when content grows
- Edges are undirected and unlabelled
- The interface is currently in Czech

## Roadmap

- [ ] Directed and labelled edges
- [ ] English interface
- [ ] Store images outside `localStorage` (IndexedDB) to lift the size ceiling
- [ ] SVG export alongside PNG
- [ ] Link a node to another map, so tabs form a graph of their own
- [ ] Present mode — step through nodes one at a time

## Related projects

- [**Flashcards**](https://github.com/SchndrDavid/flashcards) — plain-text flashcards with self-grading, for open-answer recall
- [**Tester**](https://github.com/SchndrDavid/tester) — multiple-choice tests generated from a plain `.txt` file

## Contributing

This is a personal project, but ideas and bug reports are welcome — [open an issue](https://github.com/SchndrDavid/brainmap/issues). For pull requests, please keep one change per PR.

## License

[MIT](LICENSE)
