# sethdtwigg.github.io

Personal site — [sethdtwigg.github.io](https://sethdtwigg.github.io/)

Static, hand-written HTML and CSS. **No build step, no dependencies, and no JavaScript**
(the only `<script>` on the page is a `application/ld+json` structured-data block, which
is data, not code).

## Local preview

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>. There is nothing to install or compile.

## Layout

```
index.html      the whole site
404.html        not-found page
css/style.css   @layer: tokens / base / layout / components / motion
fonts/          self-hosted woff2, latin subset
assets/         favicon, og-image, apple-touch-icon
sitemap.xml     single-URL sitemap
robots.txt
.nojekyll       serve files as-is; skip GitHub's Jekyll pass
```

## Editing

**Adding a project.** `index.html` contains a commented card template just inside the
`#work` section. Copy it, fill it in, done — there is no data file and no generation step.

**Changing colors or type scale.** Everything lives in the `@layer tokens` block at the top
of `css/style.css`. The foreground ramp (`--fg`, `--fg-muted`, `--fg-faint`) is annotated
with its contrast ratio against `--bg`; keep any replacement at 4.5:1 or better.

**Adding a contact address.** There is a commented-out block in the `#contact` section of
`index.html`. Use a dedicated forwarding alias rather than a personal inbox — a Gmail
plus-alias (`name+tag@gmail.com`) is not protection, since spammers strip the suffix to
recover the real address.

## Motion

Section and card reveals use CSS scroll-driven animations. They are deliberately additive:
the rules live inside `@supports (animation-timeline: view())`, so a browser without
support renders the page fully laid out and visible rather than leaving elements stuck at
`opacity: 0`. `prefers-reduced-motion: reduce` removes motion outright rather than
shortening it.

## Deploying

GitHub Pages serves `main` from the repository root. Push to `main` and the site rebuilds.

To add a custom domain later: add a `CNAME` file containing the bare domain, point DNS at
GitHub Pages, and update the absolute URLs in `index.html` (`og:url`, `og:image`,
`twitter:image`, `<link rel="canonical">`), `sitemap.xml`, and `robots.txt`.

## Fonts

Self-hosted rather than loaded from Google Fonts, for load speed and to avoid a
third-party request. All three are SIL Open Font License 1.1:

- **Instrument Serif** — Rodrigo Fuenzalida, Iuli Andrei
- **Inter** — Rasmus Andersson
- **JetBrains Mono** — JetBrains
