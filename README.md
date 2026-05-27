# MSP Button Maker

Tiny single-page web app that turns a citation in markdown into a downloadable
PNG "download button" matching the style used on mediastudies.press article pages.

Pure client-side: HTML/CSS for the visual, [html2canvas](https://html2canvas.hertzen.com/)
for rasterization. Designed to be hosted on GitHub Pages — no backend, no build step.

## Use

1. Open the deployed page (or `index.html` locally in a browser).
2. Paste the article's citation in markdown — e.g.
   `Author, "Title," *History of Media Studies* 5 (2025), https://doi.org/10.32376/...`
3. Click **Generate preview** to see the button.
4. Click **Download PNG** — file saves as `{slug}-button.png`.

Markdown supported:
- `*italic*` → italic
- `**bold**` → bold
- `https://…` URLs → bold dark-red link

Shortcut: Cmd/Ctrl-Enter in the textarea regenerates the preview.

## Local preview

Just open `index.html` in a browser — no server needed. Or for cleaner relative
paths use Python's tiny dev server:

```
python3 -m http.server 8000
# then open http://localhost:8000
```

## Hosting on GitHub Pages

In the repo settings → Pages → set Source to `main` branch, `/` (root). The site
will be served at `https://mediastudiespress.github.io/msp-button-maker/`.

## How it works

- The visible "button" is a normal HTML element with CSS that mirrors the Typst
  version used in HMS Process Item (2pt dark-red border, 50pt download-cloud
  icon on the left, centered Palatino citation on the right).
- `html2canvas` rasterizes that DOM node to a `<canvas>` at 3× scale, which is
  then exported as a PNG via `toDataURL`.
- All work happens in the browser. No data is uploaded anywhere.
