# Chaitalee Sohoni — chaitaleesohoni.com

Single-page holding site for Chaitalee Sohoni, illustrator and maker of things.
Static HTML + Tailwind CSS (CDN), no build step. All copy, font sizes, the
illustration path and the Instagram link live in `content.json`.

```
index.html                 the page (layout, paper texture, JSON binding script)
content.json               ALL editable content: words, font sizes, image path, links
assets/walle-watercolour.webp   the illustration shown in the bottom half of the page
```

## Editing the words, sizes or image

Open `content.json` on GitHub, press the pencil icon, change the value, commit.
GitHub Pages redeploys in about a minute.

| What you want to change        | Key in `content.json`                           |
| ------------------------------ | ----------------------------------------------- |
| Big headline                   | `hero.headline`                                 |
| Small caps line above it       | `hero.eyebrow`                                  |
| Italic line below it           | `hero.subheadline`                              |
| "Coming soon" line             | `hero.note`                                     |
| Illustration                   | `hero.image.src` (upload the file to `assets/`) and `hero.image.alt` |
| Instagram link (top right)     | `nav.instagram.url`                             |
| Name in the top-left corner    | `nav.brand`                                     |
| Footer line                    | `footer.text`                                   |
| Browser tab title / SEO text   | `site.title`, `site.description`                |
| Font sizes                     | `typography.sizes.*` — Tailwind size classes, e.g. `text-5xl md:text-7xl lg:text-8xl` |
| Fonts                          | `typography.fonts.*` — a Google Fonts URL plus the CSS `font-family` stacks |

Font-size values are plain [Tailwind font-size classes](https://tailwindcss.com/docs/font-size)
with responsive prefixes (`sm:` 640px+, `md:` 768px+, `lg:` 1024px+, `xl:` 1280px+;
`short:` is a custom prefix for landscape screens under 720px tall).

Swapping the image: drop a new JPG/PNG into `assets/`, then point `hero.image.src` at it.
The drawing is blended onto the paper with `mix-blend-mode: multiply`, so a scan or photo
with a clean white background works best. The current file was cropped and white-balanced
from the original photo so the paper disappears into the page.

## Running locally

Browsers block `fetch()` of `content.json` from a `file://` URL, so serve the folder:

```bash
python3 -m http.server 8000     # or: npx serve .
# open http://localhost:8000
```

## Deploying on GitHub Pages with the Squarespace domain

1. Push this folder to a new GitHub repository (e.g. `chaitalee-sohoni`).
2. Repo → Settings → Pages → Source: **Deploy from a branch**, branch `main`, folder `/ (root)`.
3. In Settings → Pages → Custom domain, enter the domain (e.g. `chaitaleesohoni.com`).
   GitHub will add a `CNAME` file to the repo; keep it. Tick **Enforce HTTPS** once DNS resolves.
4. In Squarespace → Domains → your domain → **DNS Settings**, add:

   | Type  | Host | Value                   |
   | ----- | ---- | ----------------------- |
   | A     | @    | 185.199.108.153         |
   | A     | @    | 185.199.109.153         |
   | A     | @    | 185.199.110.153         |
   | A     | @    | 185.199.111.153         |
   | CNAME | www  | `<github-username>.github.io` |

   Remove any existing Squarespace A/CNAME records for `@` and `www` that point at Squarespace
   hosting. DNS can take up to a few hours to propagate.
