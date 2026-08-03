# Noctilucente — Artist Site

Landing page for the Noctilucente EP, **out now**.

Noctilucent clouds only appear after the sun is gone — lit from below the
horizon, glowing at the edge of the dark. The site is built around that idea:
a near-black sky, a smouldering ember horizon, and a slow-drifting glow band.

## Tracklist

| # | Track | Credits | Status |
|---|-------|---------|--------|
| 01 | Faded Us | feat. Elina | [streaming](https://open.spotify.com/track/2WRbcYvi6TD98CgKS46Qsm) — 3:34 |
| 02 | Nobody Loved U Like I Did | feat. Elina | [streaming](https://open.spotify.com/track/0cVC50jMfvl6TOgbd05EHD) — 3:56 |
| 03 | if i became a bird | feat. Elina | [streaming](https://open.spotify.com/track/092RXsKUXJcMnNYwiDXiNN) — 4:20 |
| 04 | Afterglow | with James TW & Elina | unreleased — shows "Coming soon" |

Also on the page, in cards either side of the tracklist:
[Where We Ended](https://open.spotify.com/track/7Ldk7LUOOK2jJkKqqLD8Q9), the
first single, above it — and below it **Afterglow — the intro**, announced for
**Aug 5**. The intro is its own Spotify release, *not* track 04; the full title
track has no date yet, which is why the row above still reads "Coming soon".

The upcoming card wears silver rather than the ember badge. That is deliberate:
the palette reserves fire for music you can already play.

Each released row opens a Spotify player in place. The row is a real link to
Spotify, and the click handler only takes over when scripting is available —
so with JS off, or if anything on the page throws, the row still goes
somewhere useful. Only one player exists at a time: opening a row tears down
the previous iframe, which is what stops its audio.

**Adding track 04 when it lands.** Copy one of the released `<li>` blocks,
swap `data-track` / `data-name` / the `href` for the new Spotify id, and give
it a `track-play` mark instead of `Coming soon`. Nothing else needs touching —
the player wiring picks up any `.track[data-track]` on load.

## Stack

No build step, no dependencies. `index.html` is a single self-contained file:
markup, styles, and script all live in it. Fonts load from Google Fonts;
everything else is pure CSS.

One consequence worth knowing: it is a **single inline script**, so an
exception anywhere in it stops everything below that line. That is exactly what
took the site down after release — the countdown's `clearInterval(timer)` ran
before `const timer` was initialised, and the resulting `ReferenceError` killed
the scroll observers, leaving every section stuck at `opacity:0`. When editing
the script, prefer failing soft over throwing.

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

## Post-release state

The countdown is gone. The hero now carries the release itself — an "Out now"
badge and a play button — written into the markup rather than produced by a
script, so it renders even if nothing else runs.

All links are live: Spotify artist profile, the three released tracks, the
Where We Ended smart link (ditto.fm, all platforms), Instagram, and the
in-page players. Share previews are covered by `og.png`; favicons and
JSON-LD are in place.

Open:

- [ ] Email capture — create a free form at [formspree.io](https://formspree.io),
      then paste its endpoint into `NOTIFY_ENDPOINT` at the top of the script
      in `index.html`. The signup form reveals itself automatically, and now
      reads as "get told the moment Afterglow lands".
- [ ] **Aug 5** — when the Afterglow intro goes live, swap its card for a
      playable row (or a card with an embed) using the new Spotify id, and
      drop the `upcoming` class so it takes the ember "Out Now" badge.
- [ ] Track 04, the full Afterglow — no date yet. See the tracklist note above
      for what to change when it lands.
- [ ] `cover.jpg` has `07.23.26` set into the artwork itself, which no longer
      matches anything. Only fixable by re-exporting the cover.
