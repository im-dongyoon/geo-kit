# GEO Anti-Patterns Catalog

> When to read this: During Step 8 (Anti-Pattern Scan) of the audit workflow. Each pattern has a detection method the skill can use to find it in code.

## Severity Levels

| Level | Meaning | Icon |
|-------|---------|------|
| Critical | AI cannot access or read the content at all | 🔴 |
| Warning | AI can access but visibility/citability is degraded | 🟡 |
| Info | Suboptimal but not blocking | 🟢 |

---

## Critical Anti-Patterns

### AP-C01: Content Hidden in Modals/Tabs/Accordions
- **Severity:** 🔴 Critical
- **Affects:** All purpose types
- **Symptom:** Key content (pricing, features, FAQ answers) only renders inside interactive components (modals, accordions, tabs). AI crawlers receive collapsed/hidden HTML.
- **Detection:** Search for `Modal`, `Dialog`, `Accordion`, `Collapse`, `Tab` components containing pricing, FAQ, feature, or product description content.
- **Impact:** Content is invisible to AI — 0% citation chance for hidden content.
- **Fix:** [fix-recipes.md#AP-C01](fix-recipes.md#ap-c01)

### AP-C02: Client-Side Rendering Only (Empty HTML)
- **Severity:** 🔴 Critical
- **Affects:** All purpose types
- **Symptom:** CSR-only pages serve an empty `<div id="root">` to crawlers. All content loads via JavaScript after hydration.
- **Detection:** Check for `useEffect`-only data fetching with no SSR/SSG (`getServerSideProps`, `getStaticProps`, `generateStaticParams`, server components). Look for pages that render nothing without JS.
- **Impact:** AI receives a blank page — entire page is uncitable.
- **Fix:** [fix-recipes.md#AP-C02](fix-recipes.md#ap-c02)

### AP-C03: UUID-Only URLs
- **Severity:** 🔴 Critical
- **Affects:** All purpose types
- **Symptom:** Routes use opaque IDs (`/post/a3f2b1c4`) instead of semantic slugs (`/post/geo-optimization-guide`).
- **Detection:** Dynamic route params (e.g., `[id]`) without a corresponding slug field in data fetching or URL construction.
- **Impact:** No topical signal in URL. AI cannot infer page subject, hurting both ranking and citation.
- **Fix:** [fix-recipes.md#AP-C03](fix-recipes.md#ap-c03)

### AP-C04: Loading State Blocking Content (Next.js)
- **Severity:** 🔴 Critical
- **Affects:** Next.js App Router sites
- **Symptom:** `loading.tsx` wraps the page in Suspense. AI crawlers that don't execute JS see the loading skeleton instead of real content.
- **Detection:** Presence of `loading.tsx` or `loading.js` in route directories that serve public-facing pages.
- **Impact:** AI indexes the spinner/skeleton instead of content.
- **Fix:** [fix-recipes.md#AP-C04](fix-recipes.md#ap-c04)

### AP-C05: Noindex on Important Pages
- **Severity:** 🔴 Critical
- **Affects:** All purpose types
- **Symptom:** Key pages accidentally carry `<meta name="robots" content="noindex">` via layout inheritance or misconfiguration.
- **Detection:** Grep for `noindex` in metadata exports, `<meta>` tags, or HTTP headers on non-utility pages (exclude admin, auth, internal).
- **Impact:** AI search engines will not index or cite the page.
- **Fix:** [fix-recipes.md#AP-C05](fix-recipes.md#ap-c05)

### AP-C06: robots.txt Blocking AI Search Bots
- **Severity:** 🔴 Critical
- **Affects:** All purpose types
- **Symptom:** `robots.txt` disallows AI search crawlers (`OAI-SearchBot`, `Claude-SearchBot`, `PerplexityBot`, `GoogleOther`).
- **Detection:** Read `robots.txt` and check `User-agent` / `Disallow` rules for AI search bot names.
- **Impact:** Site is removed from AI search results entirely.
- **Fix:** [fix-recipes.md#AP-C06](fix-recipes.md#ap-c06)

---

## Warning Anti-Patterns

### AP-W01: Hardcoded JSON-LD (Not Centralized)
- **Severity:** 🟡 Warning
- **Affects:** All purpose types
- **Symptom:** Multiple inline `<script type="application/ld+json">` blocks with hardcoded brand, address, or org data scattered across pages.
- **Detection:** Count separate JSON-LD `<script>` tags across files. Check for duplicated `brand`, `address`, or `organization` literals.
- **Impact:** Maintenance burden and inconsistency risk — one stale block can confuse AI about entity identity.
- **Fix:** [fix-recipes.md#AP-W01](fix-recipes.md#ap-w01)

### AP-W02: Duplicate H1 Tags
- **Severity:** 🟡 Warning
- **Affects:** All purpose types
- **Symptom:** Multiple `<h1>` elements on a single page, often from separate mobile/desktop layouts both rendering.
- **Detection:** Count `<h1>` or `<H1>` elements per page template. Check for conditional rendering that still outputs both.
- **Impact:** AI is confused about the page's primary topic, diluting topical authority.
- **Fix:** [fix-recipes.md#AP-W02](fix-recipes.md#ap-w02)

### AP-W03: Missing lang Attribute
- **Severity:** 🟡 Warning
- **Affects:** All purpose types
- **Symptom:** No `lang` attribute on the `<html>` element.
- **Detection:** Check root layout or `_document` for `<html lang="...">`.
- **Impact:** AI may apply wrong NLP model or deprioritize in language-specific results.
- **Fix:** [fix-recipes.md#AP-W03](fix-recipes.md#ap-w03)

### AP-W04: "Contact Us" Pricing (No Real Numbers)
- **Severity:** 🟡 Warning
- **Affects:** Product, SaaS, Service pages
- **Symptom:** Pricing page says "Contact Sales" or "Request a Quote" without any visible price figures.
- **Detection:** Pricing-related pages (route or heading contains "pricing") without numeric price content (`$`, currency patterns).
- **Impact:** AI skips page in price comparisons. GPT and Perplexity read pricing pages directly — no numbers means no mention.
- **Fix:** [fix-recipes.md#AP-W04](fix-recipes.md#ap-w04)

### AP-W05: Schema-Content Type Mismatch
- **Severity:** 🟡 Warning
- **Affects:** All purpose types
- **Symptom:** JSON-LD `@type` contradicts page content (e.g., `Product` schema on a blog post, `Article` on a service page).
- **Detection:** Compare schema `@type` with page purpose detection result from heading/route analysis.
- **Impact:** Confuses AI about the content's nature, reducing trust and citation accuracy.
- **Fix:** [fix-recipes.md#AP-W05](fix-recipes.md#ap-w05)

### AP-W06: Multiple Separate JSON-LD Blocks (No @graph)
- **Severity:** 🟡 Warning
- **Affects:** All purpose types
- **Symptom:** Several separate `<script type="application/ld+json">` tags on one page instead of a single block using `@graph`.
- **Detection:** Count JSON-LD script tags per page template. Check whether `@graph` is used to group them.
- **Impact:** AI may not link related schemas together (e.g., Organization + WebPage + BreadcrumbList).
- **Fix:** [fix-recipes.md#AP-W06](fix-recipes.md#ap-w06)

### AP-W07: Static Assets Crawling Allowed
- **Severity:** 🟡 Warning
- **Affects:** All purpose types
- **Symptom:** Framework static asset directories (`/_next/static/`, `/static/`, `/assets/`) are not blocked in `robots.txt`.
- **Detection:** Check `robots.txt` for `Disallow` rules covering framework-specific static asset paths.
- **Impact:** Wastes AI crawl budget on CSS/JS files instead of content pages.
- **Fix:** [fix-recipes.md#AP-W07](fix-recipes.md#ap-w07)

### AP-W08: Missing OpenGraph Image
- **Severity:** 🟡 Warning
- **Affects:** All purpose types
- **Symptom:** No `og:image` meta tag on the page.
- **Detection:** Check for `og:image` in meta tags or `openGraph.images` in metadata exports.
- **Impact:** Reduces citation likelihood and link preview quality in AI-generated responses.
- **Fix:** [fix-recipes.md#AP-W08](fix-recipes.md#ap-w08)

---

## Info Anti-Patterns

### AP-I01: Descriptive H2 Headings (Not Question-Based)
- **Severity:** 🟢 Info
- **Affects:** Blog, FAQ, Educational content
- **Symptom:** H2 headings use noun phrases ("Marketing Landscape") instead of question form ("Why Is AI Critical for B2B Marketing?").
- **Detection:** Check H2 text for question marks or question words (`What`, `Why`, `How`, `When`, `Which`, `Where`).
- **Impact:** Lower AI citation rate — question-based H2s match user prompts more directly, improving snippet extraction.
- **Fix:** [fix-recipes.md#AP-I01](fix-recipes.md#ap-i01)

### AP-I02: Excessive Pronoun Usage
- **Severity:** 🟢 Info
- **Affects:** All purpose types
- **Symptom:** Brand or product name replaced with "we", "our", "it", "this" throughout content paragraphs.
- **Detection:** Count pronoun occurrences vs. brand/product name mentions in content sections.
- **Impact:** AI may not correctly attribute claims to the entity, reducing brand citation accuracy.
- **Fix:** [fix-recipes.md#AP-I02](fix-recipes.md#ap-i02)

### AP-I03: No dateModified Signal
- **Severity:** 🟢 Info
- **Affects:** Blog, Article, Documentation pages
- **Symptom:** No visible "Last Updated" date and no `dateModified` in structured data.
- **Detection:** Check for `dateModified` in JSON-LD schema and visible date elements on the page.
- **Impact:** AI uses freshness as a trust signal — content without recency signals gets deprioritized against dated alternatives.
- **Fix:** [fix-recipes.md#AP-I03](fix-recipes.md#ap-i03)

### AP-I04: Missing sitemap.xml
- **Severity:** 🟢 Info
- **Affects:** All purpose types
- **Symptom:** No `sitemap.xml` at site root, or sitemap exists but is outdated/incomplete.
- **Detection:** Check for `sitemap.xml` generation in project config, or `Sitemap:` directive in `robots.txt`.
- **Impact:** AI crawlers may miss pages, especially deep-linked or newly published content.
- **Fix:** [fix-recipes.md#AP-I04](fix-recipes.md#ap-i04)
