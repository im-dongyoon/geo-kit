---
name: build
description: >
  Build GEO-optimized web pages for AI search engines (ChatGPT, Perplexity,
  Google AI Overviews, Claude). Use this skill whenever the user creates or
  modifies web pages, landing pages, blog posts, FAQ sections, product pages,
  or any web content — even if they don't mention "GEO" or "SEO". Also activate
  when users mention structured data, Schema.org, JSON-LD, semantic HTML,
  meta tags, or want their content cited by AI. This skill applies to any
  framework (React, Next.js, Vue, Astro, plain HTML, etc.).
  GEO extends traditional SEO — activate for SEO-related requests too.
user-invocable: true
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

# GEO Build — Create AI-Citable Web Pages

Build web pages that AI search engines can **extract**, **understand**, and **cite**.

Traditional SEO targets Google SERP rankings. GEO targets **being cited inside AI-generated answers** — a rapidly growing channel:

- AI search traffic surged **527%** year-over-year (Previsible, 2025)
- **58%** of users prefer AI tools over traditional search (Capgemini, 2025)
- Pages with proper schema are **~2.5x more likely** to appear in AI answers (Stackmatix, 2026)

GEO and SEO are complementary. 40.58% of AI citations come from content already in Google's top 10. Layer GEO on top of SEO.

---

## Build Workflow

When building or modifying web pages, apply these steps:

1. **Detect page type** — Identify which template to follow (see Page Type Templates below)
2. **Structure content for extraction** — Apply the 7 Core Principles and Content Structure patterns
3. **Add Schema Markup** — Implement JSON-LD structured data by tier
4. **Configure AI Crawler Access** — Ensure robots.txt allows AI search bots
5. **Run pre-publish check** — Verify against the Citation Readiness Checklist

For detailed templates, read the reference files in this skill's `references/` directory (two levels up from this file: `../../references/`).

---

## 7 Core Principles for AI Citation

These conditions consistently earn AI citations.

### 1. Clean Opening Answer
The first 1-2 sentences are what AI extracts. Place a direct answer within the first 40-60 words. The first 200 words must function as a standalone, complete answer.

**Bad:** "The digital marketing landscape is rapidly changing. We offer innovative solutions."
**Good:** "[BrandName] is an AI-powered marketing automation platform for B2B SaaS. It manages email automation, lead scoring, and funnel analysis, improving conversion rates by 34%. Starting at $99/month."

### 2. Topical Completeness
Cover all major subtopics. Analyze competitor H2 headings to identify gaps. Pages with "more complete answers" earn **8x more AI citations** (Otterly, 2026).

### 3. Visible Authorship & E-E-A-T
Attach author profiles with name, credentials, and external links (LinkedIn, Crunchbase). AI uses "who wrote this" as a primary trust signal.

### 4. Crawler Accessibility
73% of websites block AI crawlers without knowing it. Allow AI search bots in robots.txt. For the full robots.txt configuration, read `../../references/ai-crawler-access.md`.

### 5. Extraction-Friendly Structure
- Use **question-based H2 headings** ("What is GEO?" not "Understanding the Environment")
- Keep paragraphs to **2-4 sentences**
- Use terminology **consistently** (same concept = same words)
- Leverage **tables, comparison frameworks, and definition blocks**

### 6. Distribution Beyond Your Site
Share on LinkedIn and communities within 48 hours. Secure at least 1 external backlink. Repurpose into multiple formats.

### 7. Post-Publish Iteration
Add fresh data, new insights, and "Last Updated" timestamps regularly. AI uses freshness as a trust signal.

---

## Content Structure Design

Design content at the **atomic fact** level — AI extracts individual paragraphs, not entire pages.

**Key patterns:**

- **Atomic Fact**: Each section answers one specific question, self-contained without surrounding context
- **Citation Block**: Place the core answer in the first 2-3 sentences of each H2. Follow with context and evidence.
- **Fact Density**: Insert specific numbers/statistics every 150-200 words. Replace "significant increase" with concrete numbers.
- **Entity Clarity**: Use the brand name explicitly — never "we", "it", "this". AI may not resolve pronoun referents.
- **Comparison Power**: Include at least 1 comparison table or framework per page.

For detailed content structure guidance with examples, read `../../references/geo-principles.md`.

---

## Page Type Templates

Detect the page type and apply the corresponding structure. For complete templates with checklists and before/after examples, read `../../references/page-templates.md`.

| Page Type | Structure |
|-----------|-----------|
| **Evergreen** (product/service) | Definition -> features -> comparison table -> pricing (real numbers) -> case studies -> FAQ |
| **Blog / Content** | Question-based H2s -> Citation Blocks -> author byline -> TL;DR -> FAQ |
| **Landing Page** | Hero definition -> problem -> features -> comparison -> testimonials -> pricing -> FAQ |
| **FAQ** | Question H2s -> 40-60 word direct answers -> FAQPage schema |
| **Pillar / Hub** | Comprehensive definition -> subtopic sections with internal links -> comparison table |

**Critical for all types:**
- H1 contains the core search query
- First 200 words work as a standalone answer
- TL;DR / Key Takeaways above the fold
- Pricing shows real numbers (not "contact us" — AI skips those)
- At least 1 comparison table
- FAQ section with FAQPage schema
- Brand name explicit, never pronouns

---

## Schema Markup

Structured data tells AI the explicit meaning of your content. **Use JSON-LD exclusively** (not microdata or RDFa).

### Tier 1 — Required on all pages

- **Organization** — Company identity (name, url, logo, description, sameAs, contactPoint)
- **BreadcrumbList** — Site structure navigation

### Tier 2 — By page type

| Page Type | Schema |
|-----------|--------|
| FAQ sections | FAQPage |
| Blog, guides | Article + Person (author) |
| Product pages | Product + AggregateOffer |
| Tutorials | HowTo |
| Services | Service + OfferCatalog |

### Tier 3 — Enhancement

- Person (author/team pages), Review/AggregateRating, Speakable (voice AI), VideoObject

For copy-paste JSON-LD templates for every schema type, read `../../references/schema-markup.md`.

**Validation:** Always validate with Google Rich Results Test and Schema Markup Validator.

---

## AI Crawler Access

AI companies operate crawlers in 3 layers: training, search indexing, and user retrieval. Blocking search bots removes you from AI search results.

**Strategy: Allow AI search bots, block training bots.**

| Action | Bots |
|--------|------|
| **Allow** (search/retrieval) | OAI-SearchBot, ChatGPT-User, Claude-SearchBot, Claude-User, PerplexityBot |
| **Block** (training) | GPTBot, ClaudeBot, Google-Extended, CCBot, Bytespider |

For the complete robots.txt configuration template, read `../../references/ai-crawler-access.md`.

**Caution:** Cloudflare's "Block AI bots" toggle blocks both training AND search bots. Use individual crawler settings instead.

---

## Platform-Specific Notes

Each AI platform has different citation patterns. For detailed strategies, read `../../references/platform-strategies.md`.

- **ChatGPT**: Prefers encyclopedic content. GPT-5.4 reads pricing pages directly — "contact us" gets skipped.
- **Perplexity**: Values recency and community references. Always cites sources, driving referral traffic.
- **Google AI Overviews**: Prioritizes content with high organic rankings and structured data.
- **Claude**: Favors E-E-A-T signals and well-structured content.

**Universal:** Include both encyclopedic definitions (for ChatGPT) and practical examples (for Perplexity). Maintain both schema markup (for Google AI) and conversational readability.

---

## Pre-Publish Quick Check

Before publishing, verify these critical items (full 31-point checklist in `../../references/citation-checklist.md`):

- [ ] First 1-2 sentences directly answer the page's core question
- [ ] First 200 words work as standalone citation
- [ ] H1 contains the target query
- [ ] All H2s are question-based
- [ ] Brand name used explicitly (no pronouns)
- [ ] At least 1 comparison table
- [ ] Specific numbers every 150-200 words
- [ ] Author byline with credentials and external links
- [ ] JSON-LD schema: Organization + BreadcrumbList (minimum)
- [ ] Page-type schema applied (FAQPage, Article, Product, etc.)
- [ ] robots.txt allows AI search bots
- [ ] Pricing shows real numbers

---

## Implementation Principles

1. **UX first** — Never sacrifice user experience for GEO optimization
2. **Content first** — Structural optimization enhances but does not replace quality content
3. **Framework agnostic** — Detect the tech stack and apply appropriate patterns
4. **Incremental** — Prioritize highest-impact changes first
5. **SEO complementary** — GEO layers on top of SEO, not replaces it
6. **Validate** — Use Google Rich Results Test and Schema Markup Validator
