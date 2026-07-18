# Noctilucente — Artist Site

Landing page for the Noctilucente EP, out **July 27**.

Noctilucent clouds only appear after the sun is gone — lit from below the
horizon, glowing at the edge of the dark. The site is built around that idea:
a near-black sky, a smouldering ember horizon, and a slow-drifting glow band.

## Tracklist

| # | Track | Credits |
|---|-------|---------|
| 01 | Faded Us | feat. Elina |
| 02 | Nobody Loved U Like I Did | feat. Elina |
| 03 | Not You | feat. Elina |
| 04 | Afterglow | with James TW & Elina |

**Out now:** [Where We Ended](https://open.spotify.com/track/7Ldk7LUOOK2jJkKqqLD8Q9)
— the latest single, featured on the page above the EP tracklist.

## Stack

No build step, no dependencies. `index.html` is a single self-contained file:
markup, styles, and the countdown script all live in it. Fonts load from Google
Fonts; everything else is pure CSS.

- **Display type** — Bodoni Moda (high-contrast Didone; the thick-to-hairline
  stroke reads as luminous)
- **Body** — Inter
- **Data / liner notes** — Space Mono
- **Surfaces** — Apple-style liquid glass (`backdrop-filter` blur + saturation,
  hairline borders, specular top edge)
- **Accent** — red → pink → fire gradient, applied to display type via
  `background-clip: text`

## Running locally

Any static server works:

```bash
python3 -m http.server 8777
# then open http://localhost:8777
```

Or just open `index.html` directly in a browser.

## Deploying to Render

`render.yaml` is a [Render Blueprint](https://render.com/docs/blueprint-spec).

1. Push this repo to GitHub.
2. In Render: **New → Blueprint**, then point it at this repository.
3. Render reads `render.yaml`, creates a static site named `noctilucente`, and
   deploys. Every push to the default branch redeploys automatically.

Pull request previews are enabled, so each PR gets its own preview URL.

## Before launch

Spotify links are live (artist profile + latest single). Two placeholders still
need real URLs — search `index.html` for `href="#"`:

- [ ] Footer — Instagram
- [ ] Footer — Apple Music

The countdown target lives at the bottom of `index.html`:

```js
const target = new Date(2026, 6, 27, 0, 0, 0).getTime();
```

Months are zero-indexed, so `6` is July. When the clock runs out the countdown
replaces itself with "Out now — go listen."
