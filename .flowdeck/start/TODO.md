# ruco-sites

One private repo (`ruco-dev/ruco-sites`) containing all Ruco project static sites. Deployed via Vercel — each subdomain maps to its own subdirectory. Shared assets (`style.css`, `main.js`, `logo.svg`) live in `ruco.dev/assets/` and are referenced by absolute URL from all project sites.

**Projects:** ruco.dev · flowdeck · mcpster · skillms · xtage · mcpill · mdblu

---

## BOT

- [ ] Scaffold repo directory structure:
  ```
  ruco-sites/
  ├── ruco.dev/
  │   ├── index.html
  │   └── assets/
  │       ├── style.css   — brand CSS (color tokens, typography, layout primitives)
  │       ├── main.js     — minimal JS (mobile nav toggle only)
  │       └── logo.svg    — Ruco wordmark placeholder
  ├── flowdeck.ruco.dev/
  │   ├── index.html
  │   └── docs/index.html
  ├── mcpster.ruco.dev/
  │   ├── index.html
  │   └── docs/index.html
  ├── skillms.ruco.dev/
  │   ├── index.html
  │   └── docs/index.html
  ├── xtage.ruco.dev/
  │   ├── index.html
  │   └── docs/index.html
  ├── mcpill.ruco.dev/
  │   ├── index.html
  │   └── docs/index.html
  ├── mdblu.ruco.dev/
  │   ├── index.html
  │   └── docs/index.html
  └── README.md
  ```

- [ ] Write `ruco.dev/assets/style.css` — shared brand styles consumed by all project sites via `https://ruco.dev/assets/style.css`

- [ ] Write per-project `index.html` (landing page: hero, 3–4 feature bullets, install/use CTA) for:
  - flowdeck, mcpster, skillms, xtage, mcpill, mdblu

- [ ] Write per-project `docs/index.html` (nav skeleton, intro paragraph, link to repo) for all 6

- [ ] Write `ruco.dev/index.html` — Ruco brand landing linking to all project sites

- [ ] Write `README.md` — repo structure docs, Vercel domain config instructions, asset URL convention

---

## HUMAN

- [ ] **Prereq:** `*.ruco.dev` wildcard DNS configured on Cloudflare (CNAME `*` → Vercel, proxy **on** — Vercel handles TLS)
- [ ] Create private `ruco-dev/ruco-sites` repo on GitHub
- [ ] Push BOT scaffold to `main`
- [ ] Connect `ruco-sites` repo to Vercel
- [ ] In Vercel project settings, add each domain and set its root directory:
  | Domain | Root Directory |
  |--------|---------------|
  | `ruco.dev` | `ruco.dev` |
  | `flowdeck.ruco.dev` | `flowdeck.ruco.dev` |
  | `mcpster.ruco.dev` | `mcpster.ruco.dev` |
  | `skillms.ruco.dev` | `skillms.ruco.dev` |
  | `xtage.ruco.dev` | `xtage.ruco.dev` |
  | `mcpill.ruco.dev` | `mcpill.ruco.dev` |
  | `mdblu.ruco.dev` | `mdblu.ruco.dev` |
- [ ] Review BOT-generated copy for all sites before publishing
- [ ] Verify: `https://ruco.dev/assets/style.css` resolves; each project site loads with shared styles; docs pages reachable

#### Open questions

- [x] What is `mcpill`? It appears in the project list and gets a full site, but has no description in any project context. Bot cannot write accurate landing copy without knowing what it does.
  > _answer:_/Users/ruco/ruco-dev/mcpill

- [x] What brand color palette should `style.css` use? If none specified, bot will pick neutral defaults and mark them as draft.
  > _answer:_check brand folder

- [x] What is the canonical Ruco tagline / one-liner for the `ruco.dev` hero? Without it, bot will draft something generic.
  > _answer:_Build less. Ship smarter.

- [x] Are GitHub repo URLs of the form `github.com/ruco-ai/<project>` for all projects? Bot will use this pattern in docs pages as placeholder links.
  > _answer:_github.com/ruco-dev/ for all projects

- [x] `sitegrow` is in the org project list but absent from the sites list here — intentional? Should it get a subdomain site later?
  > _answer:_private internal project

---

#### COMMENTS

- Repos are private — Vercel supports private repos on free tier; GitHub Pages does not.
- Vercel handles TLS automatically per domain — no cert management needed.
- Wildcard DNS on Cloudflare should point to Vercel's DNS target (provided in Vercel dashboard per domain). Proxy can be **on** since Vercel manages TLS — unlike GitHub Pages.
- `ruco.dev/assets/` doubles as the shared asset host — no separate assets repo needed.
- mdblu is already running on Fly.io (`mdblu.fly.dev`) — `mdblu.ruco.dev` is a separate static landing+docs site only, not the MCP server.
- Future: if assets need versioning, use filename convention (`style.v2.css`) and update `<link>` hrefs across all sites.
- **mcpill** (`github.com/ruco-dev/mcpill`): CLI for building, validating, and publishing MCP servers using the "pill format" — describe a server in `PILL.md`, hand to Claude, run `mcpill compile` → artifact, `mcpill run` → live server. Landing copy is now unblocked.
- **Brand / style.css**: `brand/color-scheme.css` is a complete, production-ready file — all CSS custom properties, ramps, semantic aliases, base reset, and component classes (`.card`, `.surface-ink`, `.btn-*`, `.input`, `.label`) already written and correct. The `style.css` task is a near-copy job; bot adds nav/layout utilities on top. No design decisions needed.
- **Logo**: `brand/ruco-r.svg` is the only SVG in the brand folder (the "R" mark). Scaffold spec names it `logo.svg` (wordmark placeholder) — bot copies it under that name. If a full wordmark SVG exists elsewhere, swap it in post-scaffold.
- **GitHub URLs**: confirmed `github.com/ruco-dev/<project>` for all projects. Docs pages use live links, no placeholders needed.
- **sitegrow**: private internal project — excluded entirely from this repo and the `ruco.dev` project grid.
- **Tagline**: "Build less. Ship smarter." confirmed for `ruco.dev` hero.

##### Flash analysis

All open questions are now resolved. No BOT tasks are blocked.

**Scaffold directory structure** — Mechanical. Repo root is already the working directory. No blockers.

**`style.css`** — `brand/color-scheme.css` is the complete source. Bot copies it as the base and adds nav/layout utilities only. Near-zero design work; first-deploy appearance will match the brand spec.

**Per-project `index.html`** — All 6 projects have sufficient copy context:
- **flowdeck**: Human↔AI TODO-driven workflow; `play` / `turn` commands; cards split into BOT / HUMAN sections.
- **mcpster**: TypeScript SDK for MCP servers; chainable API, Zod validation, stdio + HTTP transports, deploy CLI.
- **skillms**: Shared skill library MCP server; `analyze_url`, `commit_skill`, `contribute_skill`.
- **xtage**: Code intelligence layer; indexes repos into CODEINDEX.md / REPO.md for token-efficient Claude access.
- **mcpill**: CLI for building MCP servers from plain-English PILL.md specs — `init`, `compile`, `run`.
- **mdblu**: Structured Markdown templates for AI workflows (`MISSION`, `SPEC`, `ADR`, `HANDOFF`); MCP server included.

**Per-project `docs/index.html`** — Skeleton only. GitHub URLs confirmed as `github.com/ruco-dev/<project>` — live links, no placeholders needed.

**`ruco.dev/index.html`** — Tagline confirmed ("Build less. Ship smarter."). Project grid: 6 public sites (sitegrow excluded).

**`README.md`** — No unknowns. Vercel domain table is already in the card.