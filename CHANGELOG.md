# Changelog

## 3.0.0 (2026-04-06)

### Breaking Changes

- Audit scoring is now **purpose-aware** — different areas and weights per page type
- Citation checklist restructured: flat 34 items → Universal (12) + purpose-specific (8-12)
- Page templates reorganized with new Standing and Logic page types

### New

- **Purpose-Aware GEO** — pages classified as Content (citation), Standing (recommendation), or Logic (crawlability) with purpose-specific scoring and checklists
- **`geo-kit:spec`** — New skill to create/read/update project GEO Spec (`geo-spec/` directory with identity, page-map, target-prompts, schema-defaults, infra-status modules)
- **Page Purpose Detection** — auto-detects page purpose from file paths, code patterns, existing schemas; presents assessment with evidence for user confirmation
- **Anti-Pattern Catalog** — 18 GEO-breaking patterns (6 Critical, 8 Warning, 4 Info) with detection methods
- **Fix Recipes** — concrete fixes for each anti-pattern, classified as Auto-fixable / Guided / Manual
- **Content Signal Stack** — 5 universal signals every page must have regardless of purpose
- **Framework Pitfalls** — Next.js, SPA, Astro, SvelteKit, CMS-specific GEO traps

### Enhanced

- **schema-markup.md** — Added @graph pattern, @id cross-references, builder function pattern, Service vs Product selection criteria, dynamic data patterns
- **ai-crawler-access.md** — Added framework static asset blocking, llms.txt guide, noindex strategy
- **page-templates.md** — Added Standing (Product, Pricing, About/Team) and Logic (Dynamic/Data) page templates
- **Audit report** — Now includes page purpose declaration, Anti-Patterns Detected section, purpose-specific Health Card, fix-type classifications in Priority Actions

### New Reference Documents

- `references/page-purpose-detection.md` — Three-purpose taxonomy and detection algorithm
- `references/content-signal-stack.md` — Universal minimum GEO signals
- `references/anti-patterns.md` — GEO anti-pattern catalog
- `references/fix-recipes.md` — Anti-pattern fix recipes
- `references/framework-pitfalls.md` — Framework-specific GEO pitfalls
- `references/geo-spec.md` — GEO Spec format and usage guide

## 2.0.0 (2026-04-01)

### Breaking Changes

- Restructured to official plugin pattern (`skills/` directory)
- Removed `init` skill — replaced by `build` skill with auto-detect
- Skill names changed: `geo-kit:build`, `geo-kit:audit`

### New

- `geo-kit:build` — Create GEO-optimized web pages with auto-detection for page creation requests
- `geo-kit:audit` — Audit existing pages with 100-point scoring and 31-point checklist
- Each SKILL.md is self-contained with key GEO content inlined
- Pushy descriptions for better auto-triggering

### Fixed

- Skill discovery failure (root SKILL.md missing)
- Reference file path resolution (references unreachable from subdirectories)
- Skill name namespace duplication (`geo-kit:geo-kit:*`)

## 1.0.0 (2026-03-24)

### Initial Release

- SKILL.md with GEO audit & build workflows
- 6 reference guides:
  - Core principles & content structure design
  - Page type templates with checklists and before/after examples
  - Schema markup (JSON-LD) implementation guide
  - AI crawler access management
  - Platform-specific optimization strategies & KPIs
  - 31-Point Citation Readiness Checklist
