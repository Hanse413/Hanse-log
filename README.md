# hanse.log

A daily log. One markdown file per day.

## Daily workflow

1. Copy `src/content/log/_template.md` to `src/content/log/YYYY-MM-DD.md`
2. Fill in `title`, `date`, optional `tags`, write the entry
3. `git add . && git commit -m "log: 2026-06-13" && git push`

The site rebuilds and deploys automatically. Day numbers (DAY 001, 002, …)
are computed from chronological order — nothing to maintain.

## Local development

```bash
npm install
npm run dev        # http://localhost:4321
npm run build      # production build → dist/
```

Requires Node 18.17+ (Node 20+ recommended).

## First-time deployment (one-time, ~15 min)

1. **Push to GitHub**

   ```bash
   git init
   git add .
   git commit -m "initial commit"
   # create an empty repo on github.com, then:
   git remote add origin git@github.com:YOUR_USERNAME/hanse-log.git
   git push -u origin main
   ```

2. **Connect to Cloudflare Pages** (or Vercel — both work identically)
   - Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git
   - Select the repo. Framework preset: **Astro**
   - Build command: `npm run build` · Output directory: `dist`
   - Deploy. You get a free `*.pages.dev` URL immediately.

3. **Attach hanse.blog**
   - In the Pages project → Custom domains → add `hanse.blog`
   - If the domain is registered at Cloudflare, DNS is configured automatically.
     Otherwise, add the CNAME record it shows you at your registrar.
   - HTTPS is provisioned automatically. Done.

## Structure

```
src/
├── content/log/        ← your entries live here (one .md per day)
│   └── _template.md    ← copy this each day (never published)
├── layouts/Base.astro  ← page shell, fonts, masthead
├── pages/
│   ├── index.astro     ← the ledger (entry list)
│   └── log/[...slug].astro  ← individual entry pages
└── styles/global.css   ← all design tokens and styles
```

## Customizing

- Colors, fonts, spacing: everything is a CSS variable at the top of
  `src/styles/global.css`
- Tagline and masthead: `src/layouts/Base.astro`
- Site URL: `astro.config.mjs`
