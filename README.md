# sinematasayi.com

My personal website: one page, plain HTML and CSS, no framework, no build step and no JavaScript.
It is hosted for free on GitHub Pages and lives at **https://sinematasayi.com**.

**Only the `docs/` folder goes online.** Everything in it is the website; everything outside it (this README, `CLAUDE.md`) stays on GitHub only and can't be opened on sinematasayi.com. Edit a file in `docs/`, push it, and about a minute later it's live.

---

## What's where

```
sinematasayi.github.io/
├── README.md             ← this guide (not on the website)
├── CLAUDE.md             ← safety rules for working on this repo (not on the website)
└── docs/                 ← THE WEBSITE: everything in here is published
    ├── index.html            ← the home page: all text, sections and links
    ├── impressum.html        ← legal notice (German)
    ├── datenschutz.html      ← privacy policy (German)
    ├── 404.html              ← "Oups" page shown for addresses that don't exist
    ├── favicon.ico           ← tab icon for older browsers
    ├── CNAME                 ← tells GitHub Pages to use sinematasayi.com
    ├── .nojekyll             ← empty file: "serve my files as they are"
    └── assets/
        ├── css/
        │   ├── tokens.css    ← the "dials": colours, fonts, text sizes, spacing
        │   ├── base.css      ← font loading and default text styles
        │   ├── layout.css    ← page frame, grid, nav, buttons, footer
        │   ├── sections.css  ← hero, the five pillars, story, closing
        │   └── legal.css     ← Impressum and Datenschutz pages
        ├── fonts/            ← self-hosted fonts + their licences
        ├── icons/            ← favicon.svg, apple-touch-icon.png ("SA." mark)
        └── images/
            └── og-image.png  ← preview card for shared links (1200 × 630)
```

GitHub Pages is set to publish from **branch `main`, folder `/docs`** (repo → Settings → Pages).

---

## Preview the site on my Mac

**Why:** check changes before anyone else sees them.

1. Open **Terminal** and go to the website folder (`docs`):
   ```
   cd ~/github-sinem/sinematasayi.github.io/docs
   ```
2. Start a small local web server:
   ```
   python3 -m http.server 8000
   ```
3. Open **http://localhost:8000** in the browser.
4. After every change, reload with **Cmd + Shift + R** (a "hard reload" that skips the browser's saved copy).
5. When done, go back to Terminal and press **Ctrl + C** to stop the server.

Starting the server inside `docs/` matters: the site expects `docs/` to be its top folder. Opening `index.html` by double-clicking also works for a quick look, but fonts can fail to load that way, so the local server is more reliable.

---

## Common edits

| I want to… | Open this file | What to look for |
|---|---|---|
| Change text or a link on the home page | `docs/index.html` | Each part is marked with a comment like `<!-- ===== 03 / THE ESSAYS ===== -->`. Use **Cmd + F** to find the sentence. |
| Change a colour, text size or spacing | `docs/assets/css/tokens.css` | Named values like `--cobalt` or `--text-base`. Change once, updates everywhere. |
| Change how a section looks | `docs/assets/css/sections.css` | Blocks marked `HERO`, `THE STORY`, `THE FIVE PILLARS`, `CLOSING`. |
| Change the nav, buttons or footer | `docs/assets/css/layout.css` | Blocks marked `Nav`, `Buttons`, `Footer`. |
| Update the Impressum or privacy policy | `docs/impressum.html`, `docs/datenschutz.html` | The text sits between the `<main>` tags. |
| Change the tab icon | `docs/assets/icons/` + `docs/favicon.ico` | Replace the files, keeping the same names. |
| Change the link preview image | `docs/assets/images/og-image.png` | Replace with a new 1200 × 630 image, same name. |

### Example: add the link to 02 / The Side Project

In `docs/index.html`, search for `PLACEHOLDER: link to be added`. Replace the line below it:

```html
<p class="pillar__end pillar__soon">Coming soon</p>
```

with (put the real address and wording in):

```html
<p class="pillar__end"><a class="link-arrow" href="https://THE-LINK">Link text <span aria-hidden="true">→</span></a></p>
```

### Text sizes at a glance

All text sizes follow one ratio (×1.2 per step), defined in `docs/assets/css/tokens.css`:

| Step | Size (phone → laptop) | Used for |
|---|---|---|
| `--text-sm` | 14px | links, buttons |
| `--text-base` | 16 → 17px | body text, story, "More" text |
| `--text-lg` | 18 → 20px | subtitles, hero and closing text |
| `--text-xl` | 24 → 32px | story chapter titles |

Colours: white `#FFFFFF`, ink `#111111`, muted grey `#5C5C5C`, cobalt `#0F52BB`, butter cream `#F7EDD3`, divider grey `#E8E8E8`.

---

## Publish a change

I work on the branch `build-v1` and publish by sending it to `main`, which is what GitHub Pages serves.

1. **See what changed:**
   ```
   git status
   ```
   Run this from the project folder (`~/github-sinem/sinematasayi.github.io`), not from `docs/`.
2. **Check the safety rules** in `CLAUDE.md`: no keys or passwords, no phone number, postal address only in the legal pages.
3. **Save a snapshot (commit):**
   ```
   git add docs/index.html     (or whichever files changed)
   git commit -m "Short description of the change"
   ```
4. **Publish:**
   ```
   git push origin build-v1:main
   git branch -f main build-v1
   ```
   The second line keeps my local `main` in step with GitHub.
5. **Check:** after about a minute, open https://sinematasayi.com and press **Cmd + Shift + R**.
   GitHub keeps cached copies for up to 10 minutes, so a change can take a few minutes to show everywhere.

---

## Privacy: keep it this way

The privacy policy says this site uses **no cookies, no tracking and no third-party content**. Everything (fonts, icons, images) is hosted here, so visitors' browsers only ever talk to this site.

**Before adding** analytics, embedded videos or posts (YouTube, Instagram, Substack), external fonts, or any script from another site: don't, or update `docs/datenschutz.html` first.

Links that visitors click (GitHub, Substack, Instagram, LinkedIn) are fine; the privacy policy covers them.

---

## If something looks wrong

- **My change doesn't show up:** hard-reload with **Cmd + Shift + R**. On the live site, wait up to 10 minutes (cache).
- **"Address already in use" when starting the preview:** a server is already running. Use that one, or start on another port: `python3 -m http.server 8001` and open http://localhost:8001.
- **A page suddenly has no styling:** a CSS link in the `<head>` is probably broken. Compare it with `docs/index.html`.
- **I want to undo my last commit before publishing:** `git reset --soft HEAD~1` takes the commit back but keeps my edits.

---

## Fonts

Self-hosted, trimmed to English and Western European characters (WOFF2), each with its licence in `docs/assets/fonts/`:

- **Bricolage Grotesque**: headlines
- **Geist**: body text
- **Geist Mono**: uppercase labels, numbers, nav and footer

All are free, open-source fonts (SIL Open Font License).
