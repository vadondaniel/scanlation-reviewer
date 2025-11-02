# Manga Chapter Viewer

A single-page, local-first reader for manga or comic translation work. Drop in a chapter folder and the app pairs page images with multilingual scripts so you can proof read translations alongside the artwork.

## Features
- Works entirely offline in the browser - no build step or server needed.
- Reads `en.md`, `jp.md`, `hu.md` (or any subset) and adds quick language toggles.
- Supports multiple image variants (for example raw, cleaned, typeset) via subfolders.
- Responsive layout with a draggable divider between page art and notes.
- Auto/light/dark themes, adjustable text size, and keyboard shortcuts for fast navigation.
- Parses simple Markdown for per-page notes (headings, lists, bold, italic, code, links).

## Getting Started
1. Open `index.html` in a desktop browser such as Chrome, Edge, or Firefox.
2. Click the chapter title in the top-left corner and choose a chapter folder from your drive.
3. Use the navigation buttons or arrow keys to flip pages. Toggle languages or image sets from the header controls.

Tip: Because the viewer is fully client-side you can double-click `index.html`, or serve it via `live-server` or `npx serve` if you prefer a local web server.

## Folder Layout

Place the viewer (this repo) anywhere, then organise each chapter folder like:

````text
Chapter 04/
|-- en.md          # English script
|-- jp.md          # Japanese reference (optional)
|-- hu.md          # Hungarian translation (optional)
|-- 1.jpg          # Page images (any .jpg/.jpeg/.png/.webp)
|-- 2.jpg
|-- cleaned/       # Optional alternative image set
    |-- 1.jpg
    |-- 2.jpg
````

- Image files can be named `1.jpg`, `01.png`, `1-2.webp`, etc. Numeric prefixes control page order; `1-2` is useful for double spreads.
- Subfolders beneath the chapter (for example `cleaned/`, `typeset/`) become selectable image sets. The first set is treated as `Original`.

## Markdown Script Format

Each language file is a lightweight Markdown document:

````markdown
# Chapter 04 - The Abandoned Elf

## Page 1
Dialogue line one.

- Bullet points become list items.
- Use **bold** or *italic* for emphasis.

## Page 2
Second page text here.
````

Rules:
- The first `# Heading` is used as the chapter title.
- Start every page section with a `## Page N` heading. `## N` or `## N. oldal` also work.
- Content under a page heading is rendered as HTML and paired with that page image.
- Blank lines split paragraphs; two spaces before a newline insert a `<br>`.

## Keyboard Shortcuts
- Left Arrow / Right Arrow: Previous or next page.
- 0-9: Jump to a proportional position in the chapter.
- E, J, H: Switch language (when available).
- I: Cycle image sets (if more than one).
- O / L: Increase or decrease the note font size.
- P: Reset the note font size.

## Customisation Notes
- Theme mode cycles through auto -> light -> dark; auto follows your operating system preference.
- Drag the vertical bar between the image and text panes to resize them.
- Viewer width and font size preferences persist for the active session. Theme mode is stored in `localStorage`.
- To add another language, duplicate the entry pattern in the `languages` array inside `index.html` (code + markdown filename + button id + shortcut).

## Contributing
This is currently a single HTML file. If you plan to extend it, consider breaking the script into modules and adding tests or linting. Pull requests are welcome.

