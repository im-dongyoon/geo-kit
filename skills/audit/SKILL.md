---
name: geo-kit:audit
description: >
  Audit web pages for GEO (Generative Engine Optimization) readiness.
  Detects page purpose (Content/Standing/Logic), then applies purpose-specific
  scoring criteria. Scans structured data, semantic HTML, meta tags, AI crawler
  access, content citability, and anti-patterns. Produces a scored report
  (100-point scale) with a purpose-aware checklist and prioritized action items.
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

The audit applies **purpose-specific criteria** — a blog post, a pricing page, and an API route each have different GEO ceilings and are scored differently.

## Scope Detection

| Invocation | Scope |
|------------|-------|
| `/geo-kit:audit` | Full project — all pages, robots.txt, sitemap, global schema |
| `/geo-kit:audit src/pages/landing.tsx` | Single file — that page only |
| `/geo-kit:audit src/pages/` | Directory — all pages under that path |

---

## Audit Workflow

### Step -1: GEO Spec Check

Check if a `geo-spec/` directory exists at the project root.

**If exists:** Load the spec modules (identity, page-map, schema-defaults, etc.) for use in subsequent steps. The Page Map enables instant purpose detection in Step 0.

**If missing:** Inform the user:
```
이 프로젝트에 GEO Spec이 없습니다.
`/geo-kit:spec create`로 프로젝트 GEO 설정을 생성하면
브랜드명, 페이지 용도, 스키마 기본값 등을 자동으로 참조할 수 있습니다.

스펙 없이 audit을 진행할까요?
```

If proceeding without spec, continue to Step 0 with heuristic detection only.

---

### Step 0: Page Purpose Detection

Determine each page's purpose before scoring. For detailed detection signals, read `../../references/page-purpose-detection.md`.

**Three purpose types:**

| Purpose | Goal | What AI Does |
|---------|------|-------------|
| **Content** | Citation | AI quotes this page as a source |
| **Standing** | Recommendation | AI recommends this product/service |
| **Logic** | Crawlability | AI can access and read the data |

**Detection flow:**

1. **GEO Spec Page Map** — if the spec exists and has a matching path, use it directly (highest confidence)
2. **File path patterns** — `/blog/` → Content, `/pricing/` → Standing, `/api/` → Logic
3. **Code patterns** — author fields → Content, pricing components → Standing, SSR handlers → Logic
4. **Existing schema** — Article → Content, Product → Standing, none → Logic

**Present assessment to user:**

For single files:
```
이 페이지는 [상설페이지 — 제품 소개]로 보입니다.

근거:
- 파일 경로: /pricing/ 디렉토리
- 코드 패턴: PricingTable 컴포넌트, 가격 데이터 배열
- 스키마: Product 스키마 존재

맞나요? (Content / Standing / Logic 중 다른 유형이면 알려주세요)
```

For multi-file audits:
```
총 12개 페이지 분석:
- Content: 7개 (/blog/*, /guides/*)
- Standing: 4개 (/pricing, /about, /product, /features)
- Logic: 1개 (/api/*)

확인해주세요. 변경이 필요한 페이지가 있으면 알려주세요.
```

After confirmation, if `geo-spec/page-map.md` exists, offer to update it with any new mappings.

---

### Steps 1–7: Purpose-Aware Scoring

Score each page out of 100, using **different areas and weights per purpose type**.

#### Scoring by Purpose

**Content pages** — optimized for AI citation:

| Area | Score | Focus |
|------|-------|-------|
| Structured Data | /15 | Tier 1/2/3 schema coverage |
| Semantic HTML | /15 | H1, hierarchy, question-based H2s, landmarks |
| Content Citability | /20 | Opening answer, standalone 200 words, atomic facts, fact density, author |
| Meta & OpenGraph | /10 | Title, description, OG tags, dates |
| AI Crawler Access | /15 | robots.txt, AI bots, sitemap |
| Content Structure | /15 | Paragraph length, terminology, tables, definitions, pricing |
| Freshness Signals | /10 | Published date, last modified, currency |
| **Total** | **/100** | |

**Standing pages** — optimized for AI recommendation:

| Area | Score | Focus |
|------|-------|-------|
| Structured Data | /15 | Product/Service schema, Organization, @graph |
| Semantic HTML | /10 | H1, hierarchy, landmarks |
| Entity & Recommendation | /20 | Brand clarity, pricing visibility, comparison tables, competitive positioning, CTA transparency |
| Meta & OpenGraph | /10 | Title, description, OG tags |
| AI Crawler Access | /15 | robots.txt, AI bots, sitemap |
| Content Structure | /15 | Paragraph length, terminology, tables, definitions, pricing |
| Content Citability | /10 | Opening definition, standalone excerpt |
| Freshness Signals | /5 | Last modified date |
| **Total** | **/100** | |

**Logic pages** — optimized for AI crawlability:

| Area | Score | Focus |
|------|-------|-------|
| Crawlability & Rendering | /40 | SSR complete HTML, no Suspense blocking, pre-rendered routes, clean URLs, static asset blocking |
| AI Crawler Access | /30 | robots.txt, AI bots, sitemap, noindex strategy |
| Structured Data | /10 | Appropriate schema, @graph |
| Semantic HTML | /5 | Basic structure |
| Meta & OpenGraph | /5 | Basic meta tags |
| Content Structure | /10 | Content not hidden in modals, data accessible |
| **Total** | **/100** | |

#### Scoring Detail per Area

**Structured Data (Content: 15, Standing: 15, Logic: 10)**
- Tier 1 present on all pages (Organization, BreadcrumbList): 8 pts (Content/Standing) / 5 pts (Logic)
- Tier 2 appropriate to page type: 5 pts (Content/Standing) / 3 pts (Logic)
- Tier 3 enhancements: 2 pts (all)

**Semantic HTML (Content: 15, Standing: 10, Logic: 5)**
- Correct H1 with target query: 5 pts (Content) / 4 pts (Standing) / 2 pts (Logic)
- Logical heading hierarchy: 4 pts (Content) / 3 pts (Standing) / 1 pt (Logic)
- Question-based H2s: 4 pts (Content only)
- Semantic landmarks + ARIA: 1 pt (all)
- Language declaration: 1 pt (all)

**Content Citability (Content: 20, Standing: 10, Logic: 0)**
- Clean opening answer: 5 pts (Content) / 3 pts (Standing)
- Standalone first 200 words: 3 pts (Content) / 2 pts (Standing)
- Atomic fact structure: 3 pts (Content) / 0 (Standing)
- Fact density: 3 pts (Content) / 0 (Standing)
- Entity clarity: 2 pts (Content) / 3 pts (Standing)
- Comparison content: 2 pts (Content) / 2 pts (Standing)
- Author byline with E-E-A-T: 2 pts (Content only)

**Entity & Recommendation (Standing only: 20)**
- Brand name explicit, no pronouns: 4 pts
- Pricing with real numbers visible: 5 pts
- Comparison table vs alternatives: 4 pts
- Customer results with specific metrics: 3 pts
- CTA does not hide content: 4 pts

**Crawlability & Rendering (Logic only: 40)**
- SSR/SSG producing complete HTML: 15 pts
- No Suspense/loading states hiding content: 8 pts
- Dynamic routes pre-rendered or crawlable: 7 pts
- Static assets blocked in robots.txt: 5 pts
- Clean URL structure (slugs, not UUIDs): 5 pts

**Meta & OpenGraph (Content: 10, Standing: 10, Logic: 5)**
- Title tag optimized: 3 pts (Content/Standing) / 2 pts (Logic)
- Meta description: 2 pts (all)
- OpenGraph complete: 2 pts (Content/Standing) / 0 (Logic)
- Date signals: 2 pts (Content/Standing) / 0 (Logic)
- Viewport meta tag: 1 pt (all)

**AI Crawler Access (Content: 15, Standing: 15, Logic: 30)**
- robots.txt properly configured: 8 pts (Content/Standing) / 15 pts (Logic)
- AI search bots explicitly allowed: 4 pts (Content/Standing) / 8 pts (Logic)
- sitemap.xml present and current: 3 pts (Content/Standing) / 4 pts (Logic)
- noindex strategy correct: 0 (Content/Standing) / 3 pts (Logic)

**Content Structure (Content: 15, Standing: 15, Logic: 10)**
- Paragraph length (2-4 sentences): 3 pts (all)
- Terminology consistency: 3 pts (Content/Standing) / 2 pts (Logic)
- Comparison tables: 3 pts (Content/Standing) / 0 (Logic)
- Explicit definitions: 3 pts (Content/Standing) / 2 pts (Logic)
- Real pricing data: 3 pts (Content/Standing) / 0 (Logic)
- Content not hidden in modals: 0 (Content/Standing) / 6 pts (Logic)

**Freshness Signals (Content: 10, Standing: 5, Logic: 0)**
- Published date: 3 pts (Content) / 0 (Standing)
- Last modified date: 4 pts (Content) / 3 pts (Standing)
- Content freshness: 3 pts (Content) / 2 pts (Standing)

---

### Step 8: Anti-Pattern Scan

After scoring, scan for anti-patterns defined in `../../references/anti-patterns.md`.

For each detected anti-pattern, record:
- **ID** (e.g., AP-C01)
- **Severity** (Critical / Warning / Info)
- **Description** (what was found)
- **Location** (file:line)
- **Fix Type** (Auto-fixable / Guided / Manual)

Anti-patterns are reported separately from the score — they indicate structural issues that may not be captured by the point-based scoring alone.

For fix guidance, reference `../../references/fix-recipes.md`.

For framework-specific issues, reference `../../references/framework-pitfalls.md`.

---

## GEO Audit Report Format

Produce the report in this exact structure:

```
## GEO Audit Report

**Scope:** [Full project / Single file / Directory]
**Pages scanned:** [N]
**Date:** [YYYY-MM-DD]
**Page Purpose:** [Content — 블로그 / Standing — 제품 소개 / Logic — SSR 라우트]

### Overall Score: [X/100]

### GEO Health Card

| Area | Status | Score |
|------|--------|-------|
| [Purpose-specific areas] | [pass/warn/fail] | X/[max] |
| ... | ... | ... |

### Anti-Patterns Detected

| ID | Severity | Pattern | Location | Fix Type |
|----|----------|---------|----------|----------|
| AP-C01 | 🔴 Critical | Content hidden in modal | pricing.tsx:45 | Guided |
| AP-W02 | 🟡 Warning | Duplicate H1 | about.tsx:12,18 | Auto-fixable |
| ... | ... | ... | ... | ... |

(If no anti-patterns: "No anti-patterns detected.")

### Findings

[Per-area detailed findings. For each area, list what was found,
what's missing, and specific file:line references.]

### Citation Readiness Checklist

[Run purpose-specific checklist from ../../references/citation-checklist.md.
Apply Universal (12 items) + Purpose-specific items.
Mark each item pass/fail with evidence.]

### Priority Actions

1. [Critical anti-pattern → fix first, reference fix-recipes.md]
2. [Highest impact scoring improvement]
3. [Next highest impact]
...
```

**Status thresholds:**
- Pass: >= 80% of area points
- Warn: 50-79% of area points
- Fail: < 50% of area points

---

## Multi-Purpose Project Audit

When auditing a full project with mixed page types:

1. Detect purposes for all pages (Step 0)
2. Group pages by purpose
3. Score each group with its purpose-specific criteria
4. Report per-group scores and an overall project average
5. Anti-pattern scan runs across all pages regardless of purpose

Report includes a summary table:

```
### Project Summary

| Purpose | Pages | Avg Score | Key Issues |
|---------|-------|-----------|------------|
| Content | 7 | 72/100 | Missing author bylines, weak openings |
| Standing | 4 | 58/100 | No comparison tables, "contact us" pricing |
| Logic | 1 | 85/100 | Minor: static assets not blocked |
| **Overall** | **12** | **68/100** | |
```

---

## Reference Documents

For detailed guidance during the audit, read these files from `../../references/`:

| When you need... | Read |
|-----------------|------|
| Page purpose detection signals | `page-purpose-detection.md` |
| Universal minimum signals | `content-signal-stack.md` |
| Understanding what earns AI citations | `geo-principles.md` |
| Page structure templates to compare against | `page-templates.md` |
| JSON-LD schema templates to verify implementation | `schema-markup.md` |
| Correct robots.txt configuration | `ai-crawler-access.md` |
| Per-platform optimization details | `platform-strategies.md` |
| Purpose-aware checklist | `citation-checklist.md` |
| Anti-pattern catalog and detection methods | `anti-patterns.md` |
| Fix recipes for detected anti-patterns | `fix-recipes.md` |
| Framework-specific GEO pitfalls | `framework-pitfalls.md` |
| GEO spec format (if spec exists) | `geo-spec.md` |

---

## Post-Audit: GEO Spec Update

If a `geo-spec/` directory exists, offer to update:
- **`infra-status.md`** — with the latest audit date, score, and infrastructure status
- **`page-map.md`** — with any newly detected page purpose mappings

---

## Implementation Principles

1. **Purpose first** — Detect purpose before scoring; never apply a flat checklist to all page types
2. **UX first** — Never recommend changes that sacrifice user experience
3. **Impact-ordered** — Present findings from highest to lowest impact
4. **Framework agnostic** — Detect the tech stack and give framework-appropriate advice
5. **Actionable** — Every finding must have a concrete fix, not just "improve this"
6. **Evidence-based** — Reference specific files and line numbers
7. **SEO complementary** — GEO layers on top of SEO, not replaces it
