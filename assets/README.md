# Nyelele Lab — website (v2)

A static site built on a small design system. No build step, no dependencies.
Open `index.html` in a browser and it works.

```
index.html          Home — hero, scope figure, about, featured
research.html       Themes, services, methods, projects
people.html         PI, students, alumni
publications.html   Papers with topic tags, plus data and code
news.html           Lab updates
join.html           Recruiting and how to apply
assets/style.css    The entire design system
```

---

## The design system

Everything visual comes from tokens at the top of `assets/style.css`. Change a
token and every page follows. You should rarely need to touch anything else.

**Colour.** Two sets of tokens — light (`:root`) and dark
(`:root[data-theme="dark"]`). If you change one, change its partner, or the dark
mode will drift out of sync.

| Token | Role |
|---|---|
| `--bg` | page background |
| `--bg-raised` | cards and panels |
| `--bg-sunken` | the figure well |
| `--fg` / `--fg-muted` / `--fg-faint` | text, in descending emphasis |
| `--accent` | forest green — primary |
| `--accent-2` | teal — links and data labels |
| `--d0` … `--d5` | the six-step colour ramp in the matrix figure |

**Type.** Three families, each with one job. Spectral (serif) for headings,
Inter for body text, IBM Plex Mono for small uppercase labels. Swap a family in
`--serif`, `--sans`, or `--mono` and update the Google Fonts link in each page's
`<head>`.

**Rhythm.** `--section-y` controls vertical space between sections;
`--gap` controls space inside grids; `--shell` sets the maximum page width.
All three scale with the viewport.

**Reusable pieces.** `.card`, `.rows`, `.biblio`, `.roster`, `.section__head`,
`.label`, `.btn`. Copy an existing block rather than writing new markup — that
is what keeps the pages consistent.

---

## The scope figure

The matrix on the home page is the site's signature element. **It currently
contains placeholder numbers.** Replace them before anyone sees the site.

Open `index.html`, scroll to the bottom, and find the block marked
`MATRIX FIGURE DATA`. Edit only the arrays:

```js
var COLS = ["Stormwater","Air quality","Heat","Carbon","Biodiversity","Health"];
var ROWS = ["Supply modelling","Demand & access","Trade-offs",
            "Restoration priority","Climate resilience"];

var DATA = {
  projects:     [[3,2,3,2,1,1], ...],   // one row per ROWS entry
  publications: [[4,3,2,3,1,1], ...]
};
```

Each inner array must have exactly as many numbers as there are columns, and
there must be exactly as many arrays as there are rows. The colour scale is
computed from the largest number present, so you never set colours by hand.

If the categories don't fit your work, change `COLS` and `ROWS` to whatever
does — study systems, regions, methods. The figure adapts.

To remove the figure entirely, delete the `<section>` containing
`<div id="matrix">` and the `<script>` block at the bottom of `index.html`.

---

## Editing content

Placeholders appear in `[square brackets]`. Do these first:

| What | Where |
|---|---|
| `EMAIL@virginia.edu` | footer on every page, plus `join.html` |
| `href="#"` on Scholar / GitHub links | footer on every page |
| Matrix numbers | bottom of `index.html` |
| Everything in `[brackets]` | throughout |

**Add a person:** copy one `<div class="member">…</div>` block in `people.html`.

**Add a photo:** put the file in `assets/`, then replace
`<div class="member__portrait">ADD PHOTO</div>` with:

```html
<div class="member__portrait"><img src="assets/name.jpg" alt="Full Name"></div>
```

Portraits are cropped to circles, so use a square image. Under 300 KB.

**Add a publication:** copy one `<li>…</li>` in `publications.html`. Put the DOI
in the `href`. Tags are optional — delete the `.tagrow` div if you don't want them.

---

## Dark mode

The site follows the reader's system setting, and the sun/moon button flips it
for that visit. The choice is not remembered between visits, because saving it
requires browser storage.

To add persistence, replace the theme block in the `<script>` at the bottom of
each page with a version that reads and writes `localStorage`. Works fine on
GitHub Pages; it just needs to go into all six files.

---

## Publishing

Upload every file, plus the `assets` folder, to your GitHub repository, then
Settings → Pages → Deploy from a branch → `main` → `/ (root)`.

To replace the existing site: delete the old files in the repo first, then
upload these. Committing over the top leaves orphaned files behind.

---

## When something looks wrong

**Unstyled black text on white.** The `assets` folder didn't upload.

**Changes not appearing.** Hard refresh: `Ctrl+Shift+R`, or `Cmd+Shift+R` on a Mac.

**Figure area is blank.** A JavaScript error, almost always a mismatched array
length in the matrix data. Open the browser console (F12) to see it.

**Fonts look generic.** Google Fonts is unreachable — the layout still holds,
only the typefaces fall back.
