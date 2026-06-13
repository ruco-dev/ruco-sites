# ruco-sites

One private repo containing all Ruco project static sites. Each subdomain maps to its own subdirectory. Deployed via Vercel — one project, multiple domains with different root directories.

Shared assets (`style.css`, `main.js`, `logo.svg`) live in `ruco.dev/assets/` and are referenced by absolute URL from all project sites.

---

## Directory structure

```
ruco-sites/
├── ruco.dev/               → ruco.dev
│   ├── index.html
│   └── assets/
│       ├── style.css       — brand CSS (tokens, typography, layout, components)
│       ├── main.js         — mobile nav toggle
│       └── logo.svg        — Ruco "R" mark
├── flowdeck.ruco.dev/      → flowdeck.ruco.dev
│   ├── index.html
│   └── docs/index.html
├── mcpster.ruco.dev/       → mcpster.ruco.dev
│   ├── index.html
│   └── docs/index.html
├── skillms.ruco.dev/       → skillms.ruco.dev
│   ├── index.html
│   └── docs/index.html
├── xtage.ruco.dev/         → xtage.ruco.dev
│   ├── index.html
│   └── docs/index.html
├── mcpill.ruco.dev/        → mcpill.ruco.dev
│   ├── index.html
│   └── docs/index.html
└── mdblu.ruco.dev/         → mdblu.ruco.dev
    ├── index.html
    └── docs/index.html
```

---

## Shared asset URL convention

All project sites (`*.ruco.dev`) reference assets via absolute URL:

```html
<link rel="stylesheet" href="https://ruco.dev/assets/style.css">
<script src="https://ruco.dev/assets/main.js"></script>
<img src="https://ruco.dev/assets/logo.svg">
```

`ruco.dev` itself uses root-relative paths (`/assets/style.css`).

If assets need versioning in future, use filename convention: `style.v2.css`. Update all `<link>` hrefs across project sites before removing the old file.

---

## Vercel configuration

### One project, multiple domains

Connect `ruco-dev/ruco-sites` as a single Vercel project. In Vercel project settings → **Domains**, add each domain and set its **Root Directory**:

| Domain | Root Directory |
|--------|---------------|
| `ruco.dev` | `ruco.dev` |
| `flowdeck.ruco.dev` | `flowdeck.ruco.dev` |
| `mcpster.ruco.dev` | `mcpster.ruco.dev` |
| `skillms.ruco.dev` | `skillms.ruco.dev` |
| `xtage.ruco.dev` | `xtage.ruco.dev` |
| `mcpill.ruco.dev` | `mcpill.ruco.dev` |
| `mdblu.ruco.dev` | `mdblu.ruco.dev` |

Vercel rebuilds all sites on every push to `main`. There is no per-subdirectory build isolation — all subdirectory changes trigger a full deploy.

### DNS (Cloudflare)

Wildcard DNS: `CNAME * → <vercel-cname-target>` with proxy **on**. Vercel handles TLS automatically per domain — no cert management needed.

The Vercel-provided CNAME target for each domain appears in **Project Settings → Domains** after adding the domain.

### Framework preset

None — these are plain static HTML sites. Set framework to **Other** or leave unset in Vercel project settings.

---

## Adding a new project site

1. Create `<project>.ruco.dev/index.html` and `<project>.ruco.dev/docs/index.html`.
2. Reference shared assets via `https://ruco.dev/assets/style.css` etc.
3. Add the domain to Vercel with its root directory.
4. Add a project card to `ruco.dev/index.html`.
5. Push to `main`.
