---
name: geo-kit:build
description: >
  Build GEO-optimized web pages for AI search engines (ChatGPT, Perplexity,
  Google AI Overviews, Claude). Detects page purpose (Content/Standing/Logic)
  and applies purpose-specific principles. Use this skill whenever the user
  creates or modifies web pages, landing pages, blog posts, FAQ sections,
  product pages, or any web content — even if they don't mention "GEO" or
  "SEO". Also activate when users mention structured data, Schema.org,
  JSON-LD, semantic HTML, meta tags, or want their content cited by AI.
  This skill applies to any framework (React, Next.js, Vue, Astro, plain
  HTML, etc.). GEO extends traditional SEO — activate for SEO-related
  requests too.
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

# GEO Build — Create AI-Optimized Web Pages

Build web pages that AI search engines can **extract**, **understand**, and **cite** (or recommend, depending on page purpose).

Traditional SEO targets Google SERP rankings. GEO targets **being cited inside AI-generated answers** — a rapidly growing channel:

- AI search traffic surged **527%** year-over-year (Previsible, 2025)
- **58%** of users prefer AI tools over traditional search (Capgemini, 2025)
- Pages with proper schema are **~2.5x more likely** to appear in AI answers (Stackmatix, 2026)

GEO and SEO are complementary. 40.58% of AI citations come from content already in Google's top 10. Layer GEO on top of SEO.

---

## Build Workflow

### Step -1: GEO Spec Check

Check if a `geo-spec/` directory exists at the project root.

**If exists:** Load spec modules to auto-populate:
- **identity.md** → Brand name, domain URL for schema and content
- **schema-defaults.md** → Organization @id, language, currency for JSON-LD
- **page-map.md** → Known page purposes for instant detection

**If missing:** Proceed without spec. Suggest running `/geo-kit:spec create` for future builds.

---

### Step 0: Page Purpose Detection

Determine the page's purpose before applying principles. For detailed detection signals, read `../../references/page-purpose-detection.md`.

| Purpose | Goal | Build Focus |
|---------|------|-------------|
| **Content** | AI citation | Extractable answers, author trust, fact density |
| **Standing** | AI recommendation | Entity definition, pricing, comparison, positioning |
| **Logic** | AI crawlability | SSR, clean URLs, no hidden content, crawl budget |

**Detection flow:**
1. Check GEO Spec Page Map (if exists)
2. Analyze file path patterns
3. Scan code patterns
4. Present assessment with evidence, ask user to confirm

After confirmation, apply the purpose-specific principles below.

---

### Step 1: Apply Universal Content Signal Stack

These 5 signals apply to **every page**, regardless of purpose. For details, read `../../references/content-signal-stack.md`.

1. **BreadcrumbList schema** — Add BreadcrumbList to every page
2. **H1 optimization** — Single H1 containing the page's core concept
3. **Clean Opening** — First 40-60 words state what the page is about
4. **FAQ section + FAQPage schema** — Add appropriate FAQ for the purpose type
5. **JSON-LD @graph** — Consolidate all schemas in a single @graph array

---

### Step 2: Apply Purpose-Specific Principles

#### Content Pages — Optimize for Citation

Apply the 7 Core Principles:

1. **Clean Opening Answer** — First 1-2 sentences directly answer the core question. First 200 words must function as a standalone, complete answer.
2. **Topical Completeness** — Cover all major subtopics. Pages with "more complete answers" earn **8x more AI citations** (Otterly, 2026).
3. **Visible Authorship & E-E-A-T** — Author byline with name, credentials, external links.
4. **Crawler Accessibility** — Allow AI search bots in robots.txt.
5. **Extraction-Friendly Structure** — Question-based H2 headings, 2-4 sentence paragraphs, consistent terminology, tables and frameworks.
6. **Distribution Beyond Site** — Plan sharing on LinkedIn/communities within 48 hours.
7. **Post-Publish Iteration** — Include "Last Updated" timestamps, plan regular updates.

**Content structure design** — design at the **atomic fact** level:
- Each section answers one specific question, self-contained
- Place the core answer in the first 2-3 sentences of each H2 (Citation Block)
- Insert specific numbers/statistics every 150-200 words
- Use the brand name explicitly — never "we", "it", "this"
- Include at least 1 comparison table or framework

For detailed content guidance, read `../../references/geo-principles.md`.

#### Standing Pages — Optimize for Recommendation

Focus on making AI recommend this product/service:

1. **Entity Definition** — First 40 words clearly define what this is and who it's for. Not a marketing hook — a citable definition.
2. **Pricing Visibility** — Show real numbers. AI (GPT-5.4) reads pricing pages directly. "Contact us" gets skipped.
3. **Competitive Positioning** — Include at least 1 comparison table vs alternatives. Honest, fact-based comparisons earn more AI trust.
4. **Customer Proof** — Testimonials and case studies with specific, quantified results.
5. **Schema Accuracy** — Use Service (for SaaS/subscriptions) or Product (for tangible goods), not Article. See `../../references/schema-markup.md` for selection criteria.
6. **Brand Clarity** — Use the brand/product name explicitly. AI must be able to identify the entity without ambiguity.

#### Logic Pages — Optimize for Crawlability

Focus on making the page accessible to AI crawlers:

1. **Server-Side Rendering** — Ensure all GEO-critical content is in the initial HTML response. No client-side-only rendering for public content.
2. **No Content Blocking** — Don't hide content behind modals, tabs, accordions, or Suspense/loading boundaries.
3. **Clean URLs** — Use semantic slugs, not UUIDs. Each meaningful page needs its own URL.
4. **Crawl Budget** — Block framework static assets in robots.txt. Apply noindex to utility pages.
5. **Pre-rendering** — Use generateStaticParams (Next.js) or equivalent for dynamic routes.
6. **Redirects** — Maintain 301 redirects for any migrated/changed URLs.

For framework-specific pitfalls, read `../../references/framework-pitfalls.md`.

---

### Step 3: Apply Page Type Template

Detect the specific page type and apply the corresponding structure from `../../references/page-templates.md`.

**Content purpose:**

| Page Type | Template |
|-----------|----------|
| Blog / Article | Question-based H2s → Citation Blocks → Author byline → TL;DR → FAQ |
| Pillar / Hub | Comprehensive definition → Subtopic sections → Comparison table → FAQ |
| FAQ | Question H2s → 40-60 word direct answers → FAQPage schema |

**Standing purpose:**

| Page Type | Template |
|-----------|----------|
| Product/Service | Entity definition → Features → Comparison → Pricing → Case studies → FAQ |
| Pricing | Pricing table → Plan comparison → Competitor pricing → FAQ |
| About/Team | Company definition → Team → Milestones → FAQ |
| Landing Page | Hero definition → Problem → Features → Comparison → Testimonials → Pricing → FAQ |

**Logic purpose:**

| Page Type | Template |
|-----------|----------|
| Dynamic/Data page | Server-rendered content → H1 → Main content → FAQ (if applicable) |

**Critical for all types:**
- H1 contains the core concept
- First 40-60 words define the page (adapted to purpose)
- FAQ section with FAQPage schema
- Brand name explicit, never pronouns
- JSON-LD @graph with appropriate schemas

---

### Step 4: Add Schema Markup

Implement JSON-LD structured data. Use `../../references/schema-markup.md` for templates.

**Use @graph pattern** — consolidate all schemas in a single script tag. If GEO Spec exists, use schema-defaults for Organization @id, language, and currency.

#### Tier 1 — Required on all pages
- **Organization** — Company identity (use @id for cross-referencing)
- **BreadcrumbList** — Site structure navigation

#### Tier 2 — By purpose and page type

| Purpose | Page Type | Schema |
|---------|-----------|--------|
| Content | Blog, guides | Article + Person (author) |
| Content | FAQ sections | FAQPage |
| Content | Tutorials | HowTo |
| Standing | Product pages | Product + AggregateOffer |
| Standing | Service pages | Service + OfferCatalog |
| Standing | About pages | Organization (comprehensive) + Person |
| Logic | Any | Appropriate type matching content |

#### Tier 3 — Enhancement
- Person, Review/AggregateRating, Speakable, VideoObject

**Builder function pattern** recommended over hardcoding. See `../../references/schema-markup.md` for the builder function template.

---

### Step 5: Anti-Pattern Prevention

Before generating code, verify no known anti-patterns are being introduced. Check against `../../references/anti-patterns.md`:

- Content not hidden in modals/tabs/accordions
- Server-side rendering for public content
- Clean URL slugs (not UUIDs)
- No loading.tsx blocking content on public pages
- Single H1 (no responsive duplicates)
- Schema type matches page purpose
- JSON-LD uses @graph pattern

---

### Step 6: Configure AI Crawler Access

Ensure robots.txt allows AI search bots. For the complete configuration, read `../../references/ai-crawler-access.md`.

**Strategy: Allow AI search bots, block training bots.**

| Action | Bots |
|--------|------|
| **Allow** | OAI-SearchBot, ChatGPT-User, Claude-SearchBot, Claude-User, PerplexityBot |
| **Block** | GPTBot, ClaudeBot, Google-Extended, CCBot, Bytespider |

**Caution:** Cloudflare's "Block AI bots" toggle blocks both training AND search bots. Use individual crawler settings instead.

---

### Step 7: Pre-Publish Check

Run the purpose-specific checklist from `../../references/citation-checklist.md`:
- **Universal** (12 items) — applies to all pages
- **+ Purpose-specific** — Content (+12), Standing (+10), or Logic (+8) items

Quick critical checks:

- [ ] First 40-60 words define what the page is about
- [ ] H1 contains the core concept
- [ ] Brand name used explicitly (no pronouns)
- [ ] FAQ section with FAQPage schema
- [ ] JSON-LD @graph with appropriate schemas
- [ ] robots.txt allows AI search bots
- [ ] No anti-patterns introduced

---

## Platform-Specific Notes

Each AI platform has different citation patterns. For detailed strategies, read `../../references/platform-strategies.md`.

- **ChatGPT**: Prefers encyclopedic content. GPT-5.4 reads pricing pages directly.
- **Perplexity**: Values recency and community references. Always cites sources.
- **Google AI Overviews**: Prioritizes high organic rankings and structured data.
- **Claude**: Favors E-E-A-T signals and well-structured content.

**Universal:** Include both encyclopedic definitions (for ChatGPT) and practical examples (for Perplexity). Maintain both schema markup (for Google AI) and conversational readability.

---

## Implementation Principles

1. **Purpose first** — Detect purpose, then apply the right principles
2. **UX first** — Never sacrifice user experience for GEO optimization
3. **Content first** — Structural optimization enhances but does not replace quality content
4. **Framework agnostic** — Detect the tech stack and apply appropriate patterns
5. **Incremental** — Prioritize highest-impact changes first
6. **SEO complementary** — GEO layers on top of SEO, not replaces it
7. **Anti-pattern aware** — Don't introduce known GEO-breaking patterns
8. **Spec-aware** — Use GEO Spec data when available for consistency
