# Chaurel.ch

Minimal landing page for chaurel.ch, hosted on GitHub Pages.

## Features

- Static HTML/CSS (no JavaScript, no build step)
- Mobile-first responsive design
- Dark mode support via `prefers-color-scheme`
- Privacy-focused: `noindex` meta tags + `robots.txt`
- Automated deployment via GitHub Actions

## Local Development

Open `index.html` directly in a browser, or use any static server:

```bash
# Python
python -m http.server 8000

# Node.js (npx)
npx serve .
```

## Deployment Setup

### 1. Create GitHub Repository

```bash
git init
git add .
git commit -m "Initial commit: landing page"
git remote add origin git@github.com:USERNAME/chaurel.git
git push -u origin main
```

### 2. Enable GitHub Pages

1. Go to **Settings** → **Pages**
2. Source: **GitHub Actions**
3. The workflow will deploy automatically on push to `main`

### 3. Configure Custom Domain

#### DNS Records (Infomaniak)

Add these A records pointing to GitHub Pages:

| Type | Name | Value           |
| ---- | ---- | --------------- |
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |

Optional: Add CNAME for `www` subdomain:

| Type  | Name | Value              |
| ----- | ---- | ------------------ |
| CNAME | www  | USERNAME.github.io |

#### GitHub Settings

1. Go to **Settings** → **Pages**
2. Enter `chaurel.ch` in **Custom domain**
3. Wait for DNS check to pass
4. Enable **Enforce HTTPS** (may take a few minutes)

## Verification

### Check noindex

View page source and verify these meta tags exist:

```html
<meta
  name="robots"
  content="noindex, nofollow, noarchive, nosnippet, noimageindex"
/>
<meta
  name="googlebot"
  content="noindex, nofollow, noarchive, nosnippet, noimageindex"
/>
```

### Check robots.txt

Visit `https://chaurel.ch/robots.txt` — should show:

```
User-agent: *
Disallow: /
```

### Test Responsiveness

- Mobile: 375px width
- Tablet: 768px width
- Desktop: 1200px width

## Limitations

`noindex` is a **request**, not a guarantee. Search engines generally respect it, but:

- Already-indexed pages may remain briefly
- Some crawlers may ignore it
- The page is still publicly accessible via direct URL

For stronger privacy, consider:

- Cloudflare (can add `X-Robots-Tag` headers)
- HTTP Basic Auth
- Private hosting

## File Structure

```
.
├── index.html           # Landing page
├── styles.css           # Styles (mobile-first, dark mode)
├── robots.txt           # Disallow all crawlers
├── CNAME                # Custom domain
├── .nojekyll            # Bypass Jekyll
├── README.md            # This file
└── .github/
    └── workflows/
        └── deploy-pages.yml  # GitHub Actions
```

## License

MIT License
