# Migrating sanjaynichani.com from Weebly to Free Static Hosting

You have the Weebly export in `sanjaynichani/`. Here are your options and what to fix before going live.

---

## Free static hosting options

| Service | Free tier | Custom domain | Best for |
|--------|-----------|---------------|----------|
| **GitHub Pages** | Yes | Yes (sanjaynichani.com) | Simple, Git-based, no account beyond GitHub |
| **Netlify** | Yes | Yes | Drag-and-drop or Git; great DX, instant previews |
| **Vercel** | Yes | Yes | Same idea as Netlify; very fast |
| **Cloudflare Pages** | Yes | Yes | Fast CDN; can use Cloudflare for DNS (you’re on Hover) |

**Recommendation:** **GitHub Pages** or **Netlify**. Both support your Hover domain, SSL, and are reliable. Use GitHub Pages if you’re fine with a Git repo; use Netlify if you want optional drag-and-drop deploy.

---

## What is Hugo?

**Hugo** is a **static site generator**, not a hosting service. You give it:

- Content (e.g. Markdown files)
- A theme and config

It **builds** a folder of static HTML/CSS/JS that you then deploy to GitHub Pages, Netlify, etc.

- **Pros:** Clean content (Markdown), fast builds, easy to add a blog, version-controlled content.
- **Cons:** Your current site is already static HTML from Weebly; moving to Hugo means redoing structure and possibly design.

So: **Hugo is optional.** You can either (1) fix and deploy your existing Weebly HTML as a static site, or (2) later rebuild the site in Hugo and deploy the same way.

---

## Two migration paths

### Path A: Use the Weebly export as a static site (fastest)

Use the HTML/CSS/JS you already have. Steps:

1. **Fix asset references** (see “What to fix in the export” below).
2. **Add missing assets:** The export references `uploads/...` and `files/templateArtifacts.js`. If those aren’t in the zip, download images/PDFs from the live site or Weebly and add an empty or minimal `templateArtifacts.js` if the script is missing.
3. **Put the site in a Git repo** (e.g. only the built static files, or the whole project).
4. **Deploy:**
   - **GitHub Pages:** Push to a repo, enable Pages, set source to main branch (e.g. `/ (root)` or `/docs` if site is in `docs/`).
   - **Netlify:** Connect the same repo and set publish directory to the folder that contains `index.html` (e.g. `sanjaynichani` or a cleaned `public`).
5. **Point your domain:** In Hover, set A/CNAME for `sanjaynichani.com` and `www` to the host’s instructions (e.g. GitHub Pages or Netlify).

Result: same look and content, no Weebly dependency, free hosting.

### Path B: Rebuild with Hugo (later, if you want)

- Create a new Hugo site, pick a theme, and copy your content into Markdown/shortcodes.
- Build with `hugo` and deploy the `public/` folder to GitHub Pages or Netlify the same way.

Use Path A first to get off Weebly quickly; consider Hugo when you want a blog or a more maintainable structure.

---

## What to fix in the Weebly export

Your pages currently depend on:

1. **Weebly CDNs** (will keep working but tie you to their URLs):
   - `http://cdn11.editmysite.com/...`, `http://cdn2.editmysite.com/fonts/...`
   - For a first pass you can leave these; the site will work. For full independence, replace with local copies or public CDNs (e.g. Google Fonts for fonts).

2. **Local paths:**
   - `files/main_style.css` and `files/theme/...` — already under `sanjaynichani/files/`. Keep the same relative structure when you deploy (e.g. deploy the whole `sanjaynichani` folder so `index.html` and `files/` sit side by side).

3. **Images and PDFs:**
   - References like `uploads/1/2/4/9/124976677/...` — the export doesn’t include an `uploads` folder. You need to either:
     - Download these from the live site (e.g. with a “save full site” tool or manually), or
     - Re-export from Weebly and ensure “include uploads” (or equivalent) is checked, then add an `uploads` folder under `sanjaynichani/` so paths like `uploads/1/2/4/9/...` resolve.

4. **Root vs subfolder:**
   - Some CSS uses `url("/uploads/...")` (leading slash = site root). If you deploy so the site is at `https://sanjaynichani.com/`, then `uploads` must be at `https://sanjaynichani.com/uploads/...`. So the folder structure on the host should be: `index.html` and `uploads/` at the same level (and `files/` next to them).

5. **Missing script:**
   - `files/templateArtifacts.js` is referenced but not in the export. The site may work without it; if something breaks (e.g. menus or animations), you can add an empty `templateArtifacts.js` or try to get it from Weebly/archive.

---

## Domain at Hover

- You’ll keep the domain at Hover and only change where it points.
- In Hover’s DNS for `sanjaynichani.com`:
  - For **GitHub Pages**: add the records they give you (e.g. A records and/or CNAME for `www`).
  - For **Netlify/Vercel/Cloudflare Pages**: add the CNAME (and any A/ALIAS) they tell you.
- After DNS propagates, the host will serve your site at sanjaynichani.com and usually provide free HTTPS.

---

## Suggested next steps

1. **Gather uploads:** Download the `uploads` folder from the live site or get it from Weebly, and place it under `sanjaynichani/uploads/` so paths match.
2. **Test locally:** Open `sanjaynichani/index.html` in a browser (or run a local server, e.g. `python3 -m http.server` in `sanjaynichani/`). Fix any broken images/PDFs and the `templateArtifacts.js` reference if needed.
3. **Create a repo:** e.g. `sanjaynichani.github.io` (for GitHub Pages) or any repo name and set the publish directory to `sanjaynichani` (or the folder that contains `index.html`).
4. **Deploy:** Enable GitHub Pages or connect the repo to Netlify and deploy.
5. **Configure domain:** In Hover, point `sanjaynichani.com` and `www` to the chosen host.

If you tell me whether you prefer GitHub Pages or Netlify and what’s in your Weebly zip (e.g. do you have `uploads` or not?), I can give exact folder layout and Hover DNS values next.
