---
name: audit
description: >
  Audit web pages for GEO (Generative Engine Optimization) readiness.
  Scans structured data, semantic HTML, meta tags, AI crawler access,
  and content citability. Produces a scored report (100-point scale)
  with a 31-point checklist and prioritized action items.
  Use this skill when users want to check, audit, evaluate, review, or
  score their pages for AI search visibility — even if they say "SEO audit"
  or just "check my site". Also activate when users ask why their content
  isn't showing up in ChatGPT, Perplexity, or Google AI Overviews.
user-invocable: true
argument-hint: "[file or directory path] — omit for full project audit"
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

# GEO Audit — Check AI Search Readiness

Scan a codebase and produce a **GEO Audit Report** scored out of 100, identifying exactly what to fix for AI search visibility.

## Scope Detection

| Invocation | Scope |
|------------|-------|
| `/geo-kit:audit` | Full project — all pages, robots.txt, sitemap, global schema |
| `/geo-kit:audit src/pages/landing.tsx` | Single file — that page only |
| `/geo-kit:audit src/pages/` | Directory — all pages under that path |

---

## Audit Workflow

### Step 1: Scan Structured Data

Search for existing JSON-LD, microdata, or RDFa across all pages in scope.

**Check for:**
- Tier 1 schemas present (Organization, BreadcrumbList) — required on every page
- Tier 2 schemas by page type (FAQPage, Article, Product, HowTo, Service)
- Tier 3 enhancement schemas (Person, AggregateRating, Speakable, VideoObject)
- JSON-LD format used (not microdata or RDFa — those cause parsing issues)
- Required fields populated (no empty or placeholder values)
- Content-schema consistency (schema data matches visible page content)

**Scoring (15 points):**
- Tier 1 present on all pages: 8 pts
- Tier 2 appropriate to page types: 5 pts
- Tier 3 enhancements: 2 pts

### Step 2: Check Heading Hierarchy & Semantic HTML

Verify semantic structure that AI uses for content extraction.

**Check for:**
- Single H1 per page containing the core search query
- Logical heading hierarchy (H1 -> H2 -> H3, no skipped levels)
- H2s in question form matching user prompts (not vague labels)
- Semantic landmarks (header, main, nav, footer, article, section)
- ARIA labels where appropriate

**Scoring (15 points):**
- Correct H1 with target query: 5 pts
- Logical heading hierarchy: 4 pts
- Question-based H2s: 4 pts
- Semantic landmarks: 2 pts

### Step 3: Evaluate Content Citability

This is the most impactful area — whether AI can actually extract and cite the content.

**Check for:**
- Clean opening answer in first 40-60 words (direct answer, not hooks or fluff)
- First 200 words function as standalone citation
- TL;DR / Key Takeaways above the fold
- Atomic fact structure (each section answers one question)
- Fact density (specific numbers every 150-200 words)
- Entity clarity (brand name explicit, no pronoun substitution)
- At least 1 comparison table or framework
- Author byline with credentials and external profile links

**Scoring (20 points):**
- Clean opening answer: 5 pts
- Standalone first 200 words: 3 pts
- Atomic fact structure: 3 pts
- Fact density: 3 pts
- Entity clarity: 2 pts
- Comparison content: 2 pts
- Author byline with E-E-A-T signals: 2 pts

### Step 4: Evaluate Meta Tags & OpenGraph

**Check for:**
- Title tag (50-60 chars, contains target query)
- Meta description (150-160 chars, compelling summary)
- OpenGraph tags (og:title, og:description, og:image, og:type)
- Published date and last modified date displayed
- Canonical URL

**Scoring (10 points):**
- Title tag optimized: 3 pts
- Meta description present: 2 pts
- OpenGraph complete: 3 pts
- Date signals present: 2 pts

### Step 5: Verify AI Crawler Access

**Check for:**
- robots.txt exists and is accessible
- AI search bots allowed: OAI-SearchBot, ChatGPT-User, Claude-SearchBot, Claude-User, PerplexityBot
- Training bots blocked: GPTBot, ClaudeBot, Google-Extended
- sitemap.xml exists and includes important pages
- No Cloudflare "Block AI bots" blanket blocking (if detectable)

For the full recommended robots.txt configuration, read `../../references/ai-crawler-access.md`.

**Scoring (15 points):**
- robots.txt properly configured: 8 pts
- AI search bots explicitly allowed: 4 pts
- sitemap.xml present and current: 3 pts

### Step 6: Check Content Structure & Formatting

**Check for:**
- Paragraphs kept to 2-4 sentences
- Consistent terminology (same concept = same word)
- Comparison information in table format
- Key terms have explicit definitions
- Pricing shows real numbers (not "contact us")

**Scoring (15 points):**
- Paragraph length: 3 pts
- Terminology consistency: 3 pts
- Comparison tables: 3 pts
- Explicit definitions: 3 pts
- Real pricing data: 3 pts

### Step 7: Check Freshness Signals

**Check for:**
- Published date displayed
- Last modified / "Last Updated" date displayed
- Content appears current (no stale data or outdated references)

**Scoring (10 points):**
- Published date: 3 pts
- Last modified date: 4 pts
- Content freshness: 3 pts

---

## GEO Audit Report Format

Produce the report in this exact structure:

```
## GEO Audit Report

**Scope:** [Full project / Single file / Directory]
**Pages scanned:** [N]
**Date:** [YYYY-MM-DD]

### Overall Score: [X/100]

### GEO Health Card

| Area | Status | Score |
|------|--------|-------|
| Structured Data | [pass/warn/fail] | X/15 |
| Semantic HTML | [pass/warn/fail] | X/15 |
| Content Citability | [pass/warn/fail] | X/20 |
| Meta & OpenGraph | [pass/warn/fail] | X/10 |
| AI Crawler Access | [pass/warn/fail] | X/15 |
| Content Structure | [pass/warn/fail] | X/15 |
| Freshness Signals | [pass/warn/fail] | X/10 |

### Findings

[Per-area detailed findings. For each area, list what was found,
what's missing, and specific file:line references.]

### 31-Point Citation Readiness Checklist

[Run per-page checklist. Mark each item pass/fail with evidence.]

### Priority Actions

1. [Highest impact action — what to fix first and why]
2. [Second highest impact]
3. [Third...]
```

**Status thresholds:**
- Pass: >= 80% of area points
- Warn: 50-79% of area points
- Fail: < 50% of area points

---

## 31-Point Citation Readiness Checklist

Run this per page. Each item is pass or fail.

### A. Opening Structure (4 points)
1. First 1-2 sentences directly answer the page's core question
2. First 200 words function as independent citation
3. Table of contents with descriptive anchor links present
4. Key Takeaways / TL;DR section above the fold

### B. Topical Completeness (6 points)
5. H1 contains the exact target query/phrase
6. All major subtopics covered (compare competitor H2s)
7. Each section answers only one specific question
8. All key terms include explicit definitions
9. Specific numbers/statistics included (not vague language)
10. At least 1 comparison table or framework present

### C. Entity Signals (4 points)
11. Brand name used explicitly (no "we", "it", "this")
12. Author byline with name, credentials, external links
13. Organization and Person schemas implemented
14. Brand/product names consistent across all pages

### D. Technical Accessibility (4 points)
15. robots.txt allows AI search bots
16. Cloudflare WAF not blocking AI search bots
17. sitemap.xml up to date
18. Satisfactory page load speed

### E. Content Formatting (7 points)
19. H2 headings in question form matching user prompts
20. Paragraphs kept to 2-4 sentences
21. Terminology used consistently
22. Comparison info structured as tables
23. FAQPage schema on FAQ sections
24. Appropriate page-type schema applied
25. Published and last modified dates displayed

### F. Distribution (3 points)
26. LinkedIn/community sharing plan within 48 hours
27. At least 1 external backlink/mention planned
28. Content repurposed into other formats

### G. Post-Publish Monitoring (3 points)
29. Brand citation testing schedule exists
30. Quarterly content update schedule planned
31. Key insights distilled into quotable summaries

---

## Reference Documents

For detailed guidance during the audit, read these files from this skill's `references/` directory (two levels up: `../../references/`):

| When you need... | Read |
|-----------------|------|
| Understanding what earns AI citations | `../../references/geo-principles.md` |
| Page structure templates to compare against | `../../references/page-templates.md` |
| JSON-LD schema templates to verify implementation | `../../references/schema-markup.md` |
| Correct robots.txt configuration | `../../references/ai-crawler-access.md` |
| Per-platform optimization details | `../../references/platform-strategies.md` |
| Full checklist with context | `../../references/citation-checklist.md` |

---

## Implementation Principles

1. **UX first** — Never recommend changes that sacrifice user experience
2. **Impact-ordered** — Present findings from highest to lowest impact
3. **Framework agnostic** — Detect the tech stack and give framework-appropriate advice
4. **Actionable** — Every finding must have a concrete fix, not just "improve this"
5. **Evidence-based** — Reference specific files and line numbers
6. **SEO complementary** — GEO layers on top of SEO, not replaces it
