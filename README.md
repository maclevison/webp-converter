# webp/convert

A lightweight, zero-dependency browser-based tool for converting PNG and JPEG images to WebP format.

No server. No installs. Just open the file.

![Static HTML](https://img.shields.io/badge/static-HTML-e8ff47?style=flat-square)
![No dependencies](https://img.shields.io/badge/dependencies-none-47ffb2?style=flat-square)
![License MIT](https://img.shields.io/badge/license-MIT-666?style=flat-square)

---

## Features

- **Drag & drop** or click to select multiple images
- **Quality slider** — choose compression level (1–100%) before converting
- **Convert individually** or all at once with a progress bar
- **Download individually** or as a **ZIP archive**
- **Size comparison** — shows how much smaller (or larger) the WebP output is vs. the original
- Runs entirely in the browser — no data leaves your machine

---

## Usage

### Local

Just open `webp-converter.html` in any modern browser. No setup required.

### Self-hosted

Upload the single HTML file to any static host:

- A DigitalOcean Droplet with Nginx
- Netlify / Vercel (drop the file)
- GitHub Pages
- Any web server serving static files

---

## How it works

Conversion uses the native browser **Canvas API**:

```js
canvas.toBlob((blob) => resolve(blob), "image/webp", quality);
```

ZIP packaging uses [JSZip](https://stphane.github.io/jszip/) loaded from CDN.  
Everything else is vanilla HTML, CSS, and JavaScript.

---

## A note on file size

WebP is not always smaller than the original. For **photos**, WebP typically achieves significant size reduction. For **logos and flat graphics**, PNG may produce smaller files since its lossless compression is optimized for that content type.

If the converted WebP is larger than the original, consider keeping the PNG.

---

## Browser support

All modern browsers are supported. The `image/webp` canvas export is available in Chrome, Edge, Firefox, and Safari 14+.

---

## License

MIT
