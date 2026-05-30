# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Zero-dependency, browser-based PNG/JPEG → WebP converter. Single static `index.html` — HTML, CSS, and JS all inline. No build step, no server, no package manager, no tests.

## Running

Open `index.html` in any modern browser. Nothing to compile or install.

## Architecture

Everything lives in `index.html` in three blocks: `<style>` (design tokens via CSS custom properties + component classes), markup, and one `<script>`.

- **Single source of truth**: `state.files[]` holds every image as `{ id, file, origBlob, webpBlob, origSize, webpSize, name }`. `state.quality` is a 0–1 float (slider is 1–100, divided by 100). DOM is rendered imperatively from this state — no framework.
- **Conversion** (`toWebP`): native Canvas API only. Loads image → draws to canvas → `canvas.toBlob(blob, "image/webp", quality)`. This is the entire conversion engine; there is no encoder library.
- **IDs**: each card gets a monotonic `idCounter` id. DOM elements are addressed by templated id strings (`conv-${id}`, `dot-${id}`, `tag-webp-${id}`, etc.). Card buttons use inline `onclick` handlers calling global functions (`convertOne`, `downloadOne`, `removeCard`) — these must stay in global scope.
- **ZIP**: only external dependency is JSZip, loaded from CDN (`<script src=...jszip...>`). Used in `downloadZip` to bundle converted blobs.
- **`updateUI()`**: central function that re-derives button enabled/disabled state and counts from `state.files`. Call it after any mutation to `state.files`.

## Conventions

- Colors/spacing come from CSS variables in `:root` (`--accent`, `--bg`, `--surface`, etc.) — reuse them rather than hardcoding.
- Fonts: IBM Plex Mono (UI/labels) and IBM Plex Sans (body), loaded via Google Fonts `@import`.
- When adding per-card UI, follow the `id-${item.id}` templating pattern and toggle visibility with the `.hidden` class.
