# Hunter Motte Portfolio — Progress

Handoff doc for Claude (or me) to pick up cold. Updated 2026-05-31.

## What this is

Personal portfolio for **huntermotte.com**. Hunter is transitioning from senior software engineer → engineering manager → higher-level tech leadership (Director / VP Eng / Head of Eng at a meaningful stage). The site needs to read as thoughtful, senior, and personally grounded — not a generic dev portfolio, not SaaS.

- **Repo:** `huntermotte/hunter-motte-portfolio` (GitHub, public)
- **Local path:** `/Users/huntermotte/Desktop/Code/hunter-motte-portfolio`
- **Live:** https://huntermotte.com
- **LinkedIn (for copy reference):** https://www.linkedin.com/in/huntermotte/ — Hunter wrote his own bio there; treat as voice reference. Profile is partially gated; basic facts I have: EM at Railinc Corp. (Cary, NC), UNC '14, recent PMP cert (Mar 2025), past roles in Greater Boston, Raleigh-Durham, Beijing.

## Stack

- **Astro 6.4** (static output)
- **Tailwind v4** (CSS-first config via `@theme` in `src/styles/global.css`)
- **MDX** for blog and work content
- **Content Collections** (Astro v5+ style with `src/content.config.ts`)
- **@astrojs/rss** for `/rss.xml`
- **@astrojs/sitemap** for `/sitemap-index.xml`
- **Deploy:** Cloudflare Workers + Static Assets (NOT Pages — Cloudflare forced this; see "Deploy quirk" below)
- **Domain + DNS:** Cloudflare Registrar
- **Fonts:** Google Fonts via `<link>` in Layout (Fraunces + IBM Plex Sans + IBM Plex Mono)

## Aesthetic — locked in, don't drift

**Direction:** modern but rustic / outdoorsy — "field journal meets workshop," NOT techy SaaS. Hunter drives a Bronco, loves the outdoors and music.

**Palette** (see `src/styles/global.css`):

| Token | Value | Use |
|---|---|---|
| `bone` | `#f5f1ea` | Background (light) |
| `coal` | `#1a1614` | Ink (light) |
| `coal-night` | `#14110f` | Background (dark, "campfire") |
| `bone-dim` | `#ede5d6` | Ink (dark) |
| `pine` | `#2d3e2c` | Primary accent (labels, links) |
| `pine-bright` | `#4a6249` | Primary accent (dark mode) |
| `rust` | `#a8542a` | Secondary accent (hover, emphasis) |
| `rust-bright` | `#c46d3d` | Secondary accent (dark mode) |
| `hairline` | `#d9d1bf` | Borders, dividers (light) |
| `hairline-night` | `#2a241e` | Borders, dividers (dark) |

**Type:**
- Display: **Fraunces** (serif, used for headlines + italic accents)
- Body: **IBM Plex Sans** (warm humanist sans)
- Mono: **IBM Plex Mono** (metadata only — dates, stack lists, NOT labels)

**Critical convention — see [feedback_label_styling.md](~/.claude/projects/-Users-huntermotte-Desktop-Code/memory/feedback_label_styling.md):**

> **Do NOT use all-caps + mono + tracked-out labels** (`▲ 01 · CURRENTLY`, `READ MORE →`). Hunter called this "too Claude Design zeitgeist." It's the dominant 2024–26 SaaS pattern and pulls the aesthetic back to where we don't want it.
>
> **Use instead:** italic Fraunces sentence-case with a trailing em-dash for section labels (`Currently —`), italic Fraunces inline with `→` arrow for CTAs (`Read more →`). Pine color for primary, default ink for secondary. Hover to rust.
>
> Mono is fine for **true data**: post dates, coordinates, stack lists. Not for navigation or section markers.

**Copy voice:** confident and smart. Restrained. Hunter rejected "Wander to Field Notes" as too forward/folksy. Simple verb phrases beat clever ones.

**Section naming (decided 2026-05-31):** the blog section is called **"Blog"** — not "Field Notes." Hunter explicitly chose the plainer term over the editorial framing. The work section is "Built", the about page is "About", the current-focus page is "Now". Don't drift back to "Field Notes."

**Nav link styling:** Plex Sans, text-sm, sentence case, hover-to-pine — NOT italic Fraunces and NOT mono caps. Nav links need to read as functional navigation, distinct from the editorial italic-serif CTAs used inline.

**Top padding under the nav:** standard pages use `pt-12 sm:pt-16` on the first `<section>` after the Layout. Detail pages (with a back link first) use `pt-10 sm:pt-14`. The 404 uses `pt-20 sm:pt-28` to stay vertically centered. Don't drift back to `pt-24 sm:pt-32` — Hunter felt that was too much breathing room between nav and content.

## File map

```
hunter-motte-portfolio/
├── PROGRESS.md                    ← this file
├── wrangler.jsonc                 ← Cloudflare config (do not delete; see Deploy quirk)
├── astro.config.mjs               ← site URL, integrations (mdx, sitemap)
├── src/
│   ├── content.config.ts          ← Zod schemas for blog + work collections
│   ├── content/
│   │   ├── blog/
│   │   │   └── hello-world.mdx          ← placeholder seed post
│   │   └── work/
│   │       └── sample-platform-team.mdx  ← placeholder seed case study
│   ├── styles/
│   │   └── global.css             ← @theme tokens, dark variant, base styles
│   ├── layouts/
│   │   └── Layout.astro           ← base shell, font loads, FOUC-safe theme init, RSS link
│   ├── components/
│   │   ├── Nav.astro              ← top nav, HM mark + links + theme toggle
│   │   ├── Footer.astro           ← copyright + socials
│   │   ├── ThemeToggle.astro      ← sun/moon, localStorage-backed
│   │   └── Prose.astro            ← typography wrapper for MDX content
│   └── pages/
│       ├── index.astro            ← home (placeholder hero + 3 recent posts)
│       ├── about.astro            ← long bio (placeholder)
│       ├── now.astro              ← current focus (placeholder)
│       ├── 404.astro              ← "Not here."
│       ├── rss.xml.ts             ← RSS feed
│       ├── blog/
│       │   ├── index.astro        ← reverse-chron post list
│       │   └── [...slug].astro    ← single post (uses Prose)
│       └── work/
│           ├── index.astro        ← case study list
│           └── [...slug].astro    ← single case study (uses Prose)
```

## Build phases — current status

1. ✅ Scaffold + Cloudflare deploy + custom domain
2. ✅ Design tokens, fonts, layout, nav, footer, dark mode, trail-marker labels
3. 🚧 **Real copy for homepage + About** ← deferred at user request; scaffolding done
4. ✅ Blog scaffolding + RSS (real posts pending)
5. ✅ Work scaffolding (real case studies pending)
6. ✅ Now + 404 scaffolding (real content pending)
7. ⬜ Polish: Pagefind search, OG images, analytics, **Bronco animation** (see below)

## Outstanding work

**Copy (phase 3, deferred):**
- Homepage hero (currently placeholder: "Engineering leader, building teams that ship...")
- About page (currently all placeholders)
- Now page (currently all placeholders)
- First real blog post to replace `hello-world.mdx`
- First real case study to replace `sample-platform-team.mdx`

To draft copy, ask Hunter the 5 questions in this conversation's history, or use these starting prompts:
1. Career arc in 3 beats (where started, most meaningful chapter, today)
2. What he leads today (team size, domain, scale)
3. 1–2 things he's most proud of leading (raw, unpolished)
4. What "higher-level tech leadership" means to him + what he'd / wouldn't take
5. The personal throughline (how he operates, what he protects, what he rejects)

He'll likely paste resume/LinkedIn text to cross-check.

**Bronco animation (phase 7):**
Hunter has a video of his Bronco driving up a mountain/hill. Two-stage plan:
- **Day one (when ready):** small Polaroid-style video tile in footer or About — low stakes, immediate personality
- **Stretch goal:** scroll-triggered SVG silhouette of a Bronco crossing a topographic ridge on the homepage. Hand-built, lightweight, iconic.

**Phase 7 polish list:**
- Pagefind static search for blog
- OG image generation (satori / @vercel/og)
- Cloudflare Web Analytics (free, no cookies)
- Subtle paper-grain texture on background (SVG noise)
- Topographic line dividers (optional motif upgrade from current hairline rules)

## Conventions to maintain

- **Edits only when needed.** Don't refactor working code. Don't add abstractions that aren't pulling weight.
- **No new docs/READMEs unless Hunter asks.** This PROGRESS.md is the exception (explicitly requested).
- **Hunter handles all git commits and pushes.** Do not run `git commit` or `git push`. See `feedback_commits.md` in memory.
- **No all-caps mono labels.** See aesthetic section above. This is the single biggest aesthetic anti-pattern for this project.
- **Copy: confident, not folksy.** "Read more" > "Wander to Field Notes". No outdoor metaphors crammed into UI strings.
- **Mono utility is fine for true data** (dates, stack, coordinates) — not for navigation, section markers, or CTAs.

## Deploy quirk (read before touching Cloudflare)

The Cloudflare project is a **Worker + Static Assets**, not a Pages project. Cloudflare deprecated/hid the standalone Pages flow and pushed Hunter into Workers when he connected the repo. This caused a problem:

The Astro framework preset auto-injected a `SESSION` KV binding without a namespace ID, triggering wrangler's experimental auto-provisioning. On every redeploy after the first, it tried to create a duplicate namespace and failed.

**Fix in place:** `wrangler.jsonc` at repo root explicitly binds SESSION to the existing namespace ID `707607455a4c487dab8f1bca04fc8b97`. Cloudflare's build reads this and skips auto-provisioning.

**Do not delete `wrangler.jsonc`.** Do not change the SESSION binding unless you understand this. The KV namespace exists but is unused — that's fine.

The build pipeline:
- `Build command: npm run build`
- `Deploy command: npx wrangler deploy`
- Cloudflare auto-deploys on push to `main`

## How to run

```bash
cd /Users/huntermotte/Desktop/Code/hunter-motte-portfolio
npm run dev      # http://localhost:4321/
npm run build    # outputs dist/
npm run preview  # serves dist/ for final check
```

## Related memory files

- `~/.claude/projects/-Users-huntermotte-Desktop-Code/memory/project_hunter_motte_portfolio.md` — points back at this file
- `~/.claude/projects/-Users-huntermotte-Desktop-Code/memory/feedback_label_styling.md` — the no-mono-caps rule with full context
- `~/.claude/projects/-Users-huntermotte-Desktop-Code/memory/feedback_commits.md` — Hunter handles commits himself
