# vocal-slice-web

The marketing site for [Vocal Slice](https://vocalslice.com) — an app that transcribes audio on your
own machine and cuts clips by selecting text.

Plain static files served by GitHub Pages at the domain in `CNAME`. No build step, no dependencies,
no framework: edit a file, push, it's live.

## Working on it

Open `index.html` directly, or serve the folder if you want absolute paths to resolve the way they do
in production:

```bash
python -m http.server 8000      # then http://localhost:8000/
```

The app repo's `run-vocal-slice` skill screenshots this site across light/dark, desktop/mobile,
Windows/macOS and with JavaScript disabled — the no-JS variant matters, because both download buttons
are in the markup and CSS hides one.

## Generated elsewhere — don't edit these by hand

Much of this repo is written into it by scripts in the **app repo** (`word-slice`, private). Editing
these here works right up until the next time a generator runs, then silently disappears.

| Path | Written by |
| --- | --- |
| `changelog.html` | `build-scripts/changelog-site.js` — `npm run changelog:site`, from `CHANGELOG.md` |
| `favicon.svg`, `favicon-16.png`, `favicon-32.png`, `apple-touch-icon.png`, `og-image.png` | `brand/build-icon.js` |
| `demo.webp`, `demo-still.png` | `brand/build-demo.mjs` |
| `press/shots/` | `brand/build-shots.mjs` |
| `press/producthunt/` | `brand/build-ph-gallery.mjs` |
| `press/video/` (incl. `cuts.json`, `narration.json`) | `brand/build-video.mjs`, narrated by `brand/build-voiceover.mjs` |

`changelog-site.js` and `build-icon.js` skip with a note when this repo isn't checked out beside the
app repo, so a release or icon build on a machine without the site still works. The `brand/` media
generators don't check — they `mkdir -p` their output path, so running one from a machine without
this repo cloned leaves a stray `vocal-slice-web/` tree next to it rather than an error.

## Maintained here

`index.html`, `privacy.html`, `styles.css`, `store-copy.md`, `CNAME`, `robots.txt`, `sitemap.xml`,
and the two `video-poster*.jpg` (hand-picked frames — no script emits them).

`sitemap.xml` is hand-written: move a `lastmod` when a page's **content** changes, not on every push.

## The hard rule

**The cookieless analytics beacon is the only external request any page may make on load.** No
third-party fonts, no CDN scripts, no embeds, no advertising or conversion pixels. `privacy.html`
describes the current setup accurately, and anything added makes it false.

## NOTES.md

Decisions that aren't obvious from the markup and are hard to reverse — why platform detection runs
inline in `<head>`, why the newsletter form must submit natively, how checkout attribution works.
Read it before changing any of those.
