# Radon Lead-Gen Sites

A monorepo of local radon lead-generation websites. One folder per site. Each site is
plain static HTML/CSS — no build step — and deploys to its own Vercel project via
GitHub auto-deploy (push to `main` → Vercel redeploys).

## Sites in this repo

| Folder | Market | Target domain |
|---|---|---|
| `dubuque/` | Radon mitigation — Dubuque, IA | dubuqueradon.com |
| `siouxcity/` | Radon mitigation — Sioux City, IA | siouxcityradon.com |
| `champaign/` | Radon mitigation — Champaign, IL | champaignradon.com |

Each folder contains: `index.html`, four service pages, `about.html`, `contact.html`,
`styles.css`, `robots.txt`, `sitemap.xml`.

---

## 1. Push this repo to GitHub

```bash
cd radon-sites
git init
git add .
git commit -m "Initial commit: 3 radon lead-gen sites"
git branch -M main
# create an empty repo named "radon-sites" on github.com first, then:
git remote add origin https://github.com/YOUR_USERNAME/radon-sites.git
git push -u origin main
```

(Or with the GitHub CLI: `gh repo create radon-sites --private --source=. --push`.)

## 2. Connect each site to Vercel (one project per folder, same repo)

For **each** site, in the Vercel dashboard:

1. **Add New… → Project → Import** the `radon-sites` repo.
2. Set **Root Directory** to the site folder (e.g. `dubuque`). This is the key step —
   it's what lets one repo drive three independent Vercel projects.
3. **Framework Preset:** Other. **Build Command:** none. **Output Directory:** leave default
   (the folder is already the site root). It's static HTML, so there's nothing to build.
4. Deploy. You'll get a `*.vercel.app` URL immediately.

Repeat for `siouxcity` and `champaign`. Because each project is scoped to its own root
directory, a push that touches only `dubuque/` redeploys only that project.

## 3. Add your custom domains

Once you've purchased the domains:

1. Open a project → **Settings → Domains → Add** (e.g. `dubuqueradon.com`).
2. Vercel shows the DNS records to set at your registrar (an `A` record to Vercel's IP,
   or a `CNAME` to `cname.vercel-dns.com`). Add them; propagation is usually minutes.
3. Vercel issues the SSL certificate automatically.

## 4. Before you go live — swap the placeholders

Search-and-replace in each site folder:

- **Phone number:** the placeholder (e.g. `(563) 239-3724` / `tel:+15632393724`) → your
  **CallRail tracking number**. This is what makes leads measurable and rentable.
- **Form endpoint:** `https://formspree.io/f/YOUR_FORM_ID` → a real
  [Formspree](https://formspree.io) form ID (or wire the form to your CRM).
- Optional: add 3–5 local photos and a favicon.

Commit and push — Vercel redeploys automatically.

---

## Adding a new city later (the scalable part)

1. Copy an existing folder: `cp -r dubuque newcity`.
2. Find-and-replace the city name, county, state, domain, phone, service-area towns, and
   the local radon stat line throughout `newcity/`.
3. Commit + push.
4. In Vercel: **Add New… → Project → Import** the same repo, **Root Directory = `newcity`**.

That's the whole loop. The shared structure means each new site is a copy + find/replace,
not a rebuild.
