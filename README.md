# GigPe Website

A static marketing site for the GigPe Android app. No build step, no backend — plain HTML, CSS, and JS.

## Project structure

```
gigpe-website/
├── index.html          Home page (hero, story blocks, features, contact)
├── privacy.html        Privacy Policy
├── terms.html          Terms & Conditions
├── 404.html            Custom "page not found" page
├── robots.txt          Tells search engines what to crawl
├── sitemap.xml          List of pages for search engines
├── netlify.toml         Netlify configuration (headers, caching)
└── assets/
    ├── css/style.css    All styling — colors, layout, everything
    ├── js/main.js       Mobile menu + footer year
    └── images/          Just the logo (gigpe-icon.png)
```

## Colors — one place to change them all

Every color on the site is a CSS variable at the top of `assets/css/style.css`:

```css
--color-primary: #0044C7;   /* the logo blue — used for buttons, links, headings, icons */
--color-bg-tint: #EEF3FE;   /* soft background behind the visual cards */
```

Change `--color-primary` and the whole site (buttons, nav links, icons, borders) updates together — there's nothing to hunt down elsewhere.

## The ride-request "screenshots"

Rather than real app screenshots (which showed a competitor's branding baked into the image), the cards under "Cab / Bike / Auto" are built with plain HTML and CSS — no image files at all. That means they're always sharp at any screen size, load instantly, and are easy to edit: search `index.html` for `ride-card` or `route-card` to change the numbers, labels, or add more cards.

## Before you deploy — find and replace

Search all files for `your-site-name.netlify.app` and replace it with your real Netlify URL once you have one (step 5 below). It appears in:
- `index.html` (Open Graph tags, canonical link, structured data)
- `privacy.html`, `terms.html` (canonical links)
- `robots.txt`, `sitemap.xml`

This isn't required for the site to work, but it makes shared links and search engine results point to the right place.

---

## Deployment guide

### 1. Create the GitHub repository

1. Go to [github.com/new](https://github.com/new).
2. Name it something like `gigpe-website`.
3. Leave it **Public** (or Private if you prefer — both work with Netlify).
4. Don't initialize with a README (you already have one) — click **Create repository**.

### 2. Push the project to GitHub

Open a terminal in the `gigpe-website` folder and run:

```bash
git init
git add .
git commit -m "Initial GigPe website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/gigpe-website.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username.

### 3. Connect GitHub to Netlify

1. Sign up or log in at [netlify.com](https://netlify.com) (you can sign in directly with your GitHub account).
2. Click **Add new site → Import an existing project**.
3. Choose **GitHub**, authorize Netlify if asked, and select your `gigpe-website` repo.
4. Build settings: leave the **build command** empty and set the **publish directory** to `.` (a single dot — the root folder). There's nothing to build.
5. Click **Deploy site**.

### 4. Deploy the website

That's it — step 3 already deploys it. Netlify will redeploy automatically every time you `git push` to the `main` branch. No manual redeploy step needed after the first setup.

### 5. Get your free Netlify URL

After deployment finishes, Netlify shows a random URL like `https://chic-panda-123abc.netlify.app`. You can rename it:

1. Go to **Site configuration → Change site name**.
2. Pick something like `gigpe-app` (if available) → your URL becomes `https://gigpe-app.netlify.app`.
3. Go back and do the find-and-replace described above with this real URL.
4. Commit and push the change — Netlify redeploys automatically.

### 6. Connect a custom domain later (optional, whenever you're ready)

1. Buy a domain from any registrar (e.g. Namecheap, GoDaddy, Google Domains).
2. In Netlify: **Site configuration → Domain management → Add a domain**.
3. Enter your domain and follow Netlify's instructions — it'll tell you exactly which DNS records to add at your registrar (usually one `A` record and one `CNAME`, or you can point your domain's nameservers to Netlify).
4. Netlify issues a free HTTPS certificate automatically once DNS is verified (can take a few minutes to a few hours).

You don't need to do this now — the free `.netlify.app` subdomain works fully, including HTTPS, for as long as you like.

---

## Making changes later

Edit the HTML/CSS files locally, then:

```bash
git add .
git commit -m "Describe your change"
git push
```

Netlify picks up the push and redeploys within a minute or two — no dashboard action needed.
