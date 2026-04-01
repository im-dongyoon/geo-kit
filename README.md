# geo-kit

**Generative Engine Optimization (GEO) for AI coding assistants.**

[한국어](./README.ko.md)

Make your web products discoverable and citable by AI search engines — ChatGPT, Perplexity, Google AI Overviews, Claude, and more.

## What is GEO?

GEO (Generative Engine Optimization) optimizes web content so AI search engines can **extract**, **understand**, and **cite** it. While SEO targets Google SERP rankings, GEO targets **being cited inside AI-generated answers**.

- AI search traffic surged **527%** year-over-year (Previsible, 2025)
- **58%** of users prefer AI tools over traditional search (Capgemini, 2025)
- Pages with proper schema are **~2.5x more likely** to appear in AI answers (Stackmatix, 2026)

## Install

### Option 1: skills.sh (all AI coding tools)

```bash
npx skills add im-dongyoon/geo-kit --skill geo-kit
```

Works with **15+ AI coding tools**: Claude Code, Cursor, Cline, GitHub Copilot, Gemini, and more via [skills.sh](https://skills.sh).

### Option 2: Claude Code Plugin Marketplace

```
/plugin marketplace add im-dongyoon/geo-kit
/plugin install geo-kit@im-dongyoon-geo-kit
```

## Usage

### `/geo-kit:build` — Create GEO-optimized web pages

```
/geo-kit:build
```

Automatically applies GEO best practices when creating or modifying web pages. Also auto-detects page creation requests — when you say "create a landing page" or "add a blog post", the skill activates and applies:

- Proper schema markup (JSON-LD)
- Semantic HTML structure with citation-friendly formatting
- AI crawler access configuration
- Content patterns that earn AI citations

### `/geo-kit:audit` — Check existing pages

```
/geo-kit:audit                          # Full project audit
/geo-kit:audit src/pages/landing.tsx    # Single page audit
/geo-kit:audit src/pages/              # Directory audit
```

Scans your codebase and produces a **GEO Audit Report** with a score out of 100:

1. Scans structured data (JSON-LD, microdata, RDFa)
2. Checks heading hierarchy & semantic HTML
3. Evaluates content citability & fact density
4. Evaluates meta tags & OpenGraph
5. Verifies AI crawler access (robots.txt)
6. Checks content structure & formatting
7. Runs 31-point citation readiness checklist
8. Outputs scored report with prioritized action items

### Natural language (auto-detected)

```
"Build a landing page for our SaaS product"
"Audit this project for GEO optimization"
"Check this page for AI search readiness"
"Add structured data to this page"
"Optimize our robots.txt for AI crawlers"
```

## What's Covered

| Area | Guide |
|------|-------|
| **Core Principles** | 7 conditions AI requires to cite your content |
| **Page Templates** | 5 page types with structure templates & checklists |
| **Schema Markup** | JSON-LD implementation (Tier 1/2/3) with copy-paste templates |
| **AI Crawler Access** | robots.txt configuration for AI search bots |
| **Platform Strategies** | ChatGPT, Perplexity, Google AI, Claude-specific optimization |
| **Citation Checklist** | 31-point pre-publish checklist |

## Project Structure

```
geo-kit/
├── skills/
│   ├── build/
│   │   └── SKILL.md                    # /geo-kit:build — create GEO-optimized pages
│   └── audit/
│       └── SKILL.md                    # /geo-kit:audit — check existing pages
├── .claude-plugin/
│   └── marketplace.json                # Claude Code marketplace config
├── references/
│   ├── geo-principles.md               # 7 citation conditions + content structure
│   ├── page-templates.md               # Page templates, checklists, before/after examples
│   ├── schema-markup.md                # JSON-LD Schema.org implementation guide
│   ├── ai-crawler-access.md            # AI crawler management + robots.txt
│   ├── platform-strategies.md          # Per-platform strategies + KPIs
│   └── citation-checklist.md           # 31-Point Citation Readiness Checklist
├── README.md
├── README.ko.md
├── LICENSE
└── CHANGELOG.md
```

## Contributing

Contributions welcome! GEO is a rapidly evolving field — if you have new data, techniques, or platform-specific insights, please open a PR.

## License

MIT
