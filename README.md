# 🔎 Trace - Privacy & Metadata Inspector

See what your files are secretly telling everyone — then strip it out.

**Trace** is a single-page web app that reveals the hidden metadata inside photos and documents: GPS coordinates, camera serial numbers, author names, software, edit history, and exact timestamps. For images it can also remove all of it and hand you back a clean copy. Everything runs **100% in your browser** — no server, no upload, no tracking.

> The photo you just sent knows where you live. This tool shows you exactly what it's giving away.

---

## Why this exists

Most people have no idea that a phone photo pins their home on a map, or that a Word assignment carries the name of whoever actually wrote it. Trace makes that invisible data visible in a few seconds, explains what each piece reveals, and teaches you how to remove it — on any device. It's built as a free educational tool for students and anyone who cares about their digital footprint.

## Features

- **Reads metadata from images, PDFs, and Word files** entirely client-side
- **GPS location** shown as coordinates with a copy button and an optional map link, flagged as high-risk
- **Camera details** — make, model, lens, settings, and unique serial numbers
- **Authorship** — author, "last modified by", company, software, computer name
- **Timestamps** — capture, creation, and modification times, plus total editing time
- **Strip & download** — removes all metadata from images and gives you a clean copy
- **A plain-English verdict** — e.g. "3 things this file reveals about you"
- **A built-in guide** — how to strip metadata on iPhone, Android, Windows, macOS, and documents, plus the one tool worth learning (ExifTool)
- **Zero dependencies to run** — just open the HTML file

## Privacy by design

Trace never sends your files anywhere. All parsing and stripping happens locally in your browser using JavaScript. There is no backend, no analytics, and no network request that includes your data. Closing or refreshing the page forgets everything instantly. You can verify this yourself by opening the Network tab in your browser's dev tools while using it — the only requests are for the app and two open-source libraries.

## Supported files

| Type | Formats | Reads | Strips in-app |
|------|---------|-------|---------------|
| Images | JPG, HEIC, PNG, WebP, TIFF | ✅ EXIF, GPS, XMP, IPTC | ✅ (HEIC: Safari only — see notes) |
| Documents | PDF | ✅ Info dictionary + XMP | ↪ manual steps provided |
| Documents | DOCX | ✅ core + app properties | ↪ manual steps provided |

## Run it locally

No build step. Clone and open:

```bash
git clone https://github.com/nvmusman-srg/Trace.git
cd Trace
```

Then just open `index.html` in a browser. (Opening via a local server also works and avoids any `file://` quirks:)

```bash
python3 -m http.server 8000
# visit http://localhost:8000
```

## Deploy to GitHub Pages

**Option A — one click:** go to **Settings → Pages**, set **Source** to *Deploy from a branch*, pick `main` and `/ (root)`, and save. Your site goes live at `https://<your-username>.github.io/Trace/`.

**Option B — automated:** this repo includes a workflow at `.github/workflows/deploy.yml`. In **Settings → Pages**, set **Source** to *GitHub Actions*. Every push to `main` then deploys automatically.

## Run fully offline (for labs & workshops)

By default the app loads two libraries from a CDN. To make it work with no internet at all:

1. Download [`exifr`](https://cdn.jsdelivr.net/npm/exifr@7.1.3/dist/full.umd.js) and [`jszip`](https://cdn.jsdelivr.net/npm/jszip@3.10.1/dist/jszip.min.js) into a `lib/` folder.
2. In `index.html`, change the two `<script src="https://cdn.jsdelivr.net/...">` tags to point at `lib/full.umd.js` and `lib/jszip.min.js`.

That's it — the app then runs from a USB stick with no network.

## How it works

- **Images** are parsed with [exifr](https://github.com/MikeKovarik/exifr), which handles EXIF, GPS, XMP and IPTC across JPEG, HEIC, PNG and TIFF.
- **DOCX** files are ZIP archives; [JSZip](https://stuk.github.io/jszip/) opens them to read `docProps/core.xml` and `docProps/app.xml`.
- **PDF** metadata is extracted by scanning the file bytes for the Info dictionary and the XMP packet.
- **Stripping** redraws an image onto an HTML `<canvas>` and re-encodes it, which discards every metadata tag while baking in the correct orientation.

## Limitations

- **HEIC stripping** only works in browsers that can decode HEIC (Safari, yes; Chrome, usually no). The app detects this and points you to ExifTool instead. HEIC *reading* works everywhere.
- **PDF/DOCX parsing** covers the common uncompressed metadata. Files with compressed or deeply nested metadata may hide more — verify with ExifTool when it matters.
- Re-encoding a JPEG to strip it causes a small, normal quality change. PNGs are re-encoded losslessly.

## Tech stack

Plain HTML, CSS, and vanilla JavaScript. No framework, no build tooling. Libraries: exifr (MIT) and JSZip (MIT/GPL).

## Contributing

Contributions are welcome, and this is a friendly project for first-time open-source contributors. See [CONTRIBUTING.md](CONTRIBUTING.md) for ideas and setup.

## Disclaimer

Trace is for education and for inspecting files you own or are authorised to inspect. Use it to protect your own privacy and to learn how metadata works.

## License

[MIT](LICENSE) © Muhammad Usman

## Acknowledgements

Built on the excellent [exifr](https://github.com/MikeKovarik/exifr) and [JSZip](https://github.com/Stuk/jszip) libraries.
