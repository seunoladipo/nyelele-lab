# Nyelele Lab website

A complete static website. No build step, no dependencies — the browser reads the
HTML directly. Open `index.html` on your computer and it works.

```
index.html          Home
research.html       Research themes, methods, projects
people.html         PI, students, alumni
publications.html   Papers, data, code
news.html           Lab updates
join.html           Recruiting + contact
assets/style.css    All styling for every page
```

---

## 1. Edit the content

Everything in square brackets `[like this]` is a placeholder waiting for you.

**Do these first — they appear on every page:**

| What | Where | Find and replace |
|---|---|---|
| Email address | `index.html`, `join.html` | `EMAIL@virginia.edu` |
| Office address | `index.html`, `join.html` | Search for `Clark Hall` |
| Scholar / social links | `index.html`, `join.html` | Search for `Google Scholar` |
| Copyright year | every page, bottom | Search for `2026` |

**Adding a person:** open `people.html`, copy one `<div class="person">…</div>`
block, paste it below, and change the name, role, and bio.

**Adding a photo:** put the image in `assets/` (e.g. `assets/charity.jpg`), then
replace `<div class="photo">ADD PHOTO</div>` with:

```html
<div class="photo"><img src="assets/charity.jpg" alt="Charity Nyelele"></div>
```

Crop photos to a 4:5 portrait and keep them under about 300 KB.

**Adding a publication:** open `publications.html`, copy one `<li>…</li>` block,
paste it at the top, and change the year, title, and journal. Put the DOI link in
the `href="#"`.

**Changing colours:** open `assets/style.css`. The first block defines every
colour used on the site. Change a value there and it updates everywhere.

---

## 2. Preview locally

Just double-click `index.html`. That is genuinely enough for a site this simple.

If you want a local server that behaves exactly like the live one:

```bash
cd path/to/this/folder
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Stop it with Ctrl+C.

---

## 3. Put it on GitHub

### Create the organization (recommended)

Do this rather than using your personal account, so the site belongs to the lab
and survives you graduating.

1. GitHub → your avatar (top right) → **Your organizations** → **New organization** → **Free**
2. Name it `nyelele-lab`
3. Invite Dr. Nyelele and set her as an **Owner**

### Create the repository

1. Inside the organization: **New repository**
2. Name it exactly `nyelele-lab.github.io` (the name must match the org name)
3. **Public** — GitHub Pages needs public repos on the free plan
4. Create

### Upload the files

The no-terminal way: on the empty repo page, click **uploading an existing file**,
drag in every file *and* the `assets` folder, then **Commit changes**.

The git way:

```bash
cd path/to/this/folder
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/nyelele-lab/nyelele-lab.github.io.git
git push -u origin main
```

### Turn on Pages

Repository → **Settings** → **Pages** → under *Build and deployment*, set
Source to **Deploy from a branch**, branch **main**, folder **/ (root)** → Save.

Wait one to two minutes. The site is live at **https://nyelele-lab.github.io**.

---

## 4. Making changes later

Edit a file, then:

```bash
git add .
git commit -m "Add spring publications"
git push
```

The live site updates within a minute. Or edit any file directly on
github.com — click the file, then the pencil icon.

---

## 5. Using a custom domain (optional)

If the lab buys a domain (around $12/year):

1. Create a file named `CNAME` in this folder containing only the domain, e.g. `nyelelelab.org`
2. At your registrar, add these DNS records:
   - Four `A` records for the apex domain pointing to `185.199.108.153`,
     `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - One `CNAME` record for `www` pointing to `nyelele-lab.github.io`
3. Repository → Settings → Pages → enter the domain → tick **Enforce HTTPS**

DNS takes anywhere from ten minutes to a day to propagate.

---

## Things that commonly go wrong

**Site is blank or unstyled.** The `assets` folder did not upload. Check that
`assets/style.css` exists in the repo.

**404 after enabling Pages.** Give it two minutes, then confirm `index.html` is
in the repository root, not inside a subfolder.

**Changes not appearing.** Hard refresh: Ctrl+Shift+R, or Cmd+Shift+R on a Mac.

**Fonts look wrong.** The fonts load from Google Fonts, so the first load needs
an internet connection. Offline, the browser falls back to system fonts and the
layout still holds.
