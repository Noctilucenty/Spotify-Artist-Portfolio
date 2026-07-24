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
| 03 | if i had wings | feat. Elina |
| 04 | Afterglow | with James TW & Elina |

**Out now:** [Where We Ended](https://open.spotify.com/track/7Ldk7LUOOK2jJkKqqLD8Q9)
— the latest single, featured on the page above the EP tracklist.

## Stack

No build step, no dependencies. `index.html` is a single self-contained file:
markup, styles, and the countdown script all live in it. Fonts load from Google
Fonts; everything else is pure CSS.

- **Display type** — Bodoni Moda (high-contrast Didone; the thick-to-hairline
  stroke reads as luminous), display sizes only
- **Body / UI** — Geist 400
- **Labels / liner notes** — Geist Mono 500
- **Surfaces** — Apple-style liquid glass (`backdrop-filter` blur + saturation,
  hairline borders, specular top edge)
- **Palette** — "cold sky, warm afterglow": the identity is noctilucent
  silver-blue (sky, glow band, ice-gradient display type, star motes), with a
  faint ember horizon. Fire survives only where the music speaks: the word
  AFTERGLOW, the Out Now badge, the primary CTA, and the release-day banner.

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

All links are live: Spotify artist profile, the Where We Ended smart link
(ditto.fm, all platforms), Instagram, and an embedded Spotify player.
Share previews are covered by `og.png`; favicons and JSON-LD are in place.

Remaining options:

- [ ] Email capture — create a free form at [formspree.io](https://formspree.io),
      then paste its endpoint into `NOTIFY_ENDPOINT` at the top of the script
      in `index.html`. The signup form reveals itself automatically.
- [ ] EP pre-save link — when the distributor issues one, swap it into the
      primary CTA so the countdown converts into day-one saves.

The countdown target lives at the bottom of `index.html`:

```js
const target = new Date(2026, 6, 27, 0, 0, 0).getTime();
```

Months are zero-indexed, so `6` is July. When the clock runs out the countdown
replaces itself with "Out now — go listen."
