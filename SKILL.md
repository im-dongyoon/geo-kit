---
name: geo
description: >
  Generative Engine Optimization (GEO) for building AI-search-optimized products.
  Use this skill when users want to optimize their website, app, or content for
  AI search engines (ChatGPT, Perplexity, Google AI Overviews, Claude).
  Also activate when users mention: structured data, Schema.org, JSON-LD,
  AI SEO, GEO, citability, semantic HTML, robots.txt for AI bots,
  or want to build/refactor for AI search visibility.
  Activate for any SEO-related request as GEO extends traditional SEO.
user-invocable: true
argument-hint: "audit | build | checklist — target URL or project path"
effort: high
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - WebFetch
  - WebSearch
---

# GEO — Generative Engine Optimization

GEO optimizes web products so AI search engines (ChatGPT, Perplexity, Google AI Overviews, Claude) can **extract**, **understand**, and **cite** your content.

Traditional SEO targets Google SERP rankings. GEO targets **being cited inside AI-generated answers**.

## GEO vs SEO

| | SEO | GEO |
|---|---|---|
| Goal | SERP ranking | Citation in AI answers |
| Unit | Whole page | Individual paragraph / atomic fact |
| Success metric | Rank, clicks, traffic | Citation frequency, Share of Voice, sentiment |
| Content requirement | Keyword density, backlinks | Semantic clarity, structured data, extractability |
| Core question | "Can this page rank?" | "Can an AI pull a fact from this page and cite it?" |

**Important**: GEO and SEO are complementary, not replacements. Writesonic's analysis of 1M+ AI Overviews found that 40.58% of AI citations come from content already in Google's top 10. Layer GEO on top of SEO.

## Why GEO Matters Now

- AI search traffic surged 527% year-over-year (Previsible, 2025)
- 58% of users now prefer AI tools over traditional search for product discovery (Capgemini, 2025)
- 64% of customers are willing to buy AI-recommended products (Master.of.Code, 2024)
- Google AI Overviews expanded to 200+ countries and 40+ languages (Google I/O 2025)
- Gartner predicts 25% of all search will shift to generative engines by 2028

---

## Two Workflows

### Workflow A: Audit & Refactor (Existing Project)

When the user has an existing codebase, follow this process:

1. **Scan structured data** — Search for existing JSON-LD, microdata, or RDFa
2. **Check heading hierarchy** — Verify semantic HTML (h1→h2→h3), landmarks, ARIA
3. **Evaluate meta tags** — Title, description, OpenGraph, article meta
4. **Verify crawler access** — Check robots.txt for AI bot permissions
5. **Assess content citability** — Check for clean opening answers, FAQ structure, fact density
6. **Produce GEO Audit Report** — Scored report with prioritized action items

### Workflow B: Build New (New Project)

When building from scratch, apply GEO principles from the start:

1. Use page templates from `references/page-templates.md`
2. Implement Schema markup per `references/schema-markup.md`
3. Configure AI crawler access per `references/ai-crawler-access.md`
4. Follow the 7 core principles below
5. Run the 31-Point Checklist before publishing

---

## 7 Core Principles for AI Citation

These are the conditions that consistently earn AI citations. See `references/geo-principles.md` for detailed guidance.

### 1. Clean Opening Answer
The first 1–2 sentences are what AI extracts for citation. Place a direct answer to the core question within the first 40–60 words. The first 200 words must function as a standalone, complete answer.

### 2. Topical Completeness
Cover all major subtopics. Analyze competitor H2 headings to identify gaps. Pages with "more complete answers" earn 8x more AI citations (Otterly, 2026).

### 3. Visible Authorship & E-E-A-T
Attach author profiles with name, credentials, and external links (LinkedIn, Crunchbase) to all content. AI uses "who wrote this" as a primary trust signal.

### 4. Crawler Accessibility
73% of websites technically block AI crawlers without knowing it. Explicitly allow AI search bots in robots.txt. See `references/ai-crawler-access.md`.

### 5. Extraction-Friendly Structure
Use question-based H2 headings. Keep paragraphs to 2–4 sentences. Use terminology consistently. Leverage tables, comparison frameworks, and definition blocks.

### 6. Distribution Beyond Your Site
Share on LinkedIn and relevant communities within 48 hours of publishing. Secure at least 1 external backlink or mention. Repurpose into multiple formats.

### 7. Post-Publish Iteration
Regularly add fresh data, new insights, and "Last Updated" timestamps. AI uses freshness as a trust signal. Track which prompts surface your brand.

---

## Content Structure Design

Design content at the **atomic fact** level. AI extracts individual paragraphs, not entire pages. See `references/geo-principles.md` for full details.

**Key patterns:**
- **Atomic Fact**: Each section answers one specific question, self-contained without surrounding context
- **Semantic Chunking**: Place the core answer in the first 2–3 sentences of each H2 (Citation Block pattern)
- **Fact Density**: Insert specific numbers/statistics every 150–200 words
- **Entity Clarity**: Use brand name explicitly instead of pronouns ("we", "it", "this")
- **Comparison Power**: Include at least 1 comparison table or framework

---

## Page Type Templates

Five page types with structure templates, checklists, and before/after examples. See `references/page-templates.md` for complete templates.

| Page Type | Key Elements |
|-----------|-------------|
| **Evergreen** (product/service) | Definition → features → comparison table → pricing (real numbers) → case studies → FAQ |
| **Blog / Content** | Question-based H2s → Citation Blocks → author byline → TL;DR → FAQ |
| **Landing Page** | Hero definition → problem → features → comparison → testimonials → pricing → FAQ |
| **FAQ** | Question H2s → 40-60 word direct answers → FAQPage schema |
| **Pillar / Hub** | Comprehensive definition → subtopic sections with internal links → comparison table |

---

## Schema Markup

Structured data tells AI systems the explicit meaning of your content. Pages with proper schema are ~2.5x more likely to appear in AI answers (Stackmatix, 2026). **Use JSON-LD exclusively.** See `references/schema-markup.md` for all templates.

**Tier 1 (Required — all pages):** Organization, BreadcrumbList
**Tier 2 (By page type):** FAQPage, Article, Product, HowTo, Service
**Tier 3 (Enhancement):** Person, Review/AggregateRating, Speakable, VideoObject

---

## AI Crawler Access

AI companies operate crawlers in 3 layers: training, search indexing, and user retrieval. Blocking search bots removes you from AI search results. See `references/ai-crawler-access.md` for the full configuration guide.

**Recommended strategy**: Allow AI search bots, block training bots.

Key bots to allow:
- `OAI-SearchBot`, `ChatGPT-User` (OpenAI search)
- `Claude-SearchBot`, `Claude-User` (Anthropic search)
- `PerplexityBot` (Perplexity search)

Key bots to block:
- `GPTBot` (OpenAI training)
- `ClaudeBot` (Anthropic training)
- `Google-Extended` (Google training)

---

## Platform-Specific Strategies

Each AI platform has different citation patterns. See `references/platform-strategies.md` for details.

- **ChatGPT**: Prefers encyclopedic content. GPT-5.4 reads pricing pages directly — "contact us" pages get skipped.
- **Perplexity**: Values recency and community references. Always cites sources, driving referral traffic.
- **Google AI Overviews**: Prioritizes content with high organic rankings and structured data.
- **Claude**: Favors E-E-A-T signals and well-structured content.

---

## GEO Audit Report Format

When producing an audit, use this structure:

```
## GEO Audit Report

### Overall Score: [X/100]

### GEO Health Card
| Area | Status | Score |
|------|--------|-------|
| Structured Data | ✅/⚠️/❌ | X/15 |
| Semantic HTML | ✅/⚠️/❌ | X/15 |
| Content Citability | ✅/⚠️/❌ | X/20 |
| Meta & OpenGraph | ✅/⚠️/❌ | X/10 |
| AI Crawler Access | ✅/⚠️/❌ | X/15 |
| Content Structure | ✅/⚠️/❌ | X/15 |
| Freshness Signals | ✅/⚠️/❌ | X/10 |

### Findings
[Detailed findings per area]

### Priority Actions
1. [Highest impact action]
2. [Second highest]
3. ...
```

---

## 31-Point Citation Readiness Checklist

Before publishing any content, run through the full checklist in `references/citation-checklist.md`. Categories:

- **A. Opening Structure** (4 points)
- **B. Topical Completeness** (6 points)
- **C. Entity Signals** (4 points)
- **D. Technical Accessibility** (4 points)
- **E. Content Formatting** (7 points)
- **F. Distribution** (3 points)
- **G. Post-Publish Monitoring** (3 points)

---

## Implementation Principles

1. **UX first** — Never sacrifice user experience for GEO optimization
2. **Content first** — Structural optimization enhances but does not replace quality content
3. **Framework agnostic** — Detect the tech stack and apply appropriate patterns
4. **Incremental** — Prioritize highest-impact changes first
5. **SEO complementary** — GEO layers on top of SEO, not replaces it
6. **Validate** — Use Google Rich Results Test and Schema Markup Validator
