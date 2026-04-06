# GEO Fix Recipes

> When to read this: When fixing anti-patterns identified by the audit. Each recipe corresponds to an anti-pattern ID from `anti-patterns.md`.

## Fix Types

| Type | Meaning | Example |
|------|---------|---------|
| **Auto-fixable** | Skill can implement directly | Schema consolidation, meta tag additions |
| **Guided** | Requires user decision, skill provides scaffold | URL slug migration, modal content extraction |
| **Manual** | Requires architectural change by developer | CSR-to-SSR migration, framework routing changes |

---

## Critical Fixes

### AP-C01: Content Hidden in Modals → Separate Pages
**Type:** Guided

**Problem:** Key content rendered inside modal/accordion. AI crawlers get collapsed HTML.

**Recipe:**
1. Identify modal/accordion content containing GEO-relevant info (pricing, features, FAQ)
2. Create dedicated pages for each content block (e.g., `/industries/[slug]`)
3. Keep the modal as a quick-view option, but ensure the full content exists on its own URL
4. Add internal links from the parent page to the new dedicated pages
5. Apply appropriate schema to the new pages

**Example:**
```
Before: /industries → modal with industry details (not crawlable)
After:  /industries → links to /industries/healthcare, /industries/fintech (crawlable)
        Modal still works for UX, but content lives on real pages
```

### AP-C02: CSR-Only → Add Server Rendering
**Type:** Manual

**Problem:** Pages fetch data only in useEffect/client-side. AI gets empty HTML.

**Recipe:**
1. Move data fetching to server:
   - Next.js App Router: use Server Components (default) or `generateStaticParams`
   - Next.js Pages Router: use `getStaticProps` or `getServerSideProps`
   - Remix: use `loader` functions
   - SvelteKit: use `+page.server.ts`
2. Ensure the initial HTML response contains the full content
3. Verify with: `curl -s URL | grep "[expected content]"`
4. Keep client-side interactivity for UX but ensure content is in initial HTML

### AP-C03: UUID URLs → Slug Migration
**Type:** Guided

**Recipe:**
1. Add a `slug` column to your database table
2. Generate slugs from existing titles (sanitize: lowercase, hyphens, no special chars)
3. Create URL rewrite middleware:
   ```
   /resource/[id-or-slug] → detect if UUID or slug → resolve to same page
   ```
4. Add 301 redirects from old UUID URLs to new slug URLs
5. Update internal links to use slug format
6. Update sitemap.xml with new URLs

### AP-C04: loading.tsx Blocking Content
**Type:** Guided

**Recipe:**
1. Identify which route segments have loading.tsx on public-facing pages
2. Option A: Remove loading.tsx from public pages (simplest)
3. Option B: Move critical content above the Suspense boundary:
   ```tsx
   // layout.tsx — content outside Suspense
   export default function Layout({ children }) {
     return (
       <main>
         <h1>Page Title</h1>
         <p>Core content AI should see...</p>
         <Suspense fallback={<Loading />}>
           {children}  {/* Dynamic content */}
         </Suspense>
       </main>
     )
   }
   ```
4. Verify: check the initial HTML response contains the critical content

### AP-C05: Noindex on Important Pages
**Type:** Auto-fixable

**Recipe:**
1. Identify pages with noindex that should be indexed
2. Remove `robots: 'noindex'` from metadata/meta tags on those pages
3. Ensure utility pages (dashboard, auth, admin, checkout) DO keep noindex
4. Pattern for identifying utility vs public pages:
   - Public: /blog/*, /pricing, /about, /product/* → should be indexed
   - Utility: /dashboard/*, /auth/*, /admin/*, /api/* → keep noindex

### AP-C06: robots.txt Blocking AI Search Bots
**Type:** Auto-fixable

**Recipe:**
1. Check robots.txt for blanket Disallow on AI bots
2. Separate search bots (allow) from training bots (block)
3. Apply the recommended configuration from `ai-crawler-access.md`
4. Key bots to ALLOW: OAI-SearchBot, ChatGPT-User, Claude-SearchBot, Claude-User, PerplexityBot
5. Key bots to BLOCK: GPTBot, ClaudeBot, Google-Extended, CCBot, Bytespider

---

## Warning Fixes

### AP-W01: Hardcoded JSON-LD → Centralized Builder
**Type:** Guided

**Recipe:**
1. Create a schema builder utility (e.g., `lib/schema.ts`):
   ```typescript
   // lib/schema.ts
   const ORG_ID = 'https://example.com/#org';
   
   export function buildOrganization() {
     return {
       '@type': 'Organization',
       '@id': ORG_ID,
       name: '[Brand]',
       url: 'https://example.com',
       logo: 'https://example.com/logo.png',
       // ... from geo-spec/schema-defaults.md
     };
   }
   
   export function buildPageSchema(type, data) {
     return {
       '@context': 'https://schema.org',
       '@graph': [
         buildOrganization(),
         buildBreadcrumb(data.breadcrumbs),
         // page-specific schema
       ]
     };
   }
   ```
2. Replace all inline JSON-LD with builder function calls
3. Single source of truth for brand info, updated in one place

### AP-W02: Duplicate H1 → Single H1 with CSS
**Type:** Auto-fixable

**Recipe:**
1. Keep one H1 in the HTML
2. Use CSS for responsive styling (not separate mobile/desktop H1s)
3. If content must differ by viewport, use CSS `display: none` on decorative variants but keep one semantic H1

### AP-W03: Missing lang Attribute
**Type:** Auto-fixable

**Recipe:** Add `lang` attribute to `<html>` element. Match the primary content language.
```html
<html lang="ko">  <!-- or "en", "ja", etc. -->
```

### AP-W04: "Contact Us" Pricing → Show Real Numbers
**Type:** Guided

**Recipe:**
1. Add at least starting prices: "Starting at $49/month"
2. Include a pricing table with plan names and prices
3. If custom pricing exists, show a range: "$49–$499/month depending on plan"
4. AI (especially GPT-5.4) reads pricing pages directly — "contact us" gets skipped

### AP-W05: Schema-Content Mismatch → Correct Schema Type
**Type:** Guided

**Recipe:**
1. Compare page purpose (from detection) with existing schema @type
2. Common corrections:
   - Blog/guide with Product schema → change to Article
   - SaaS service page with Product schema → consider Service + hasOfferCatalog
   - Company page with Article schema → change to Organization
3. See `schema-markup.md` for Service vs Product selection criteria

### AP-W06: Separate JSON-LD → @graph Consolidation
**Type:** Auto-fixable

**Recipe:**
1. Collect all separate `<script type="application/ld+json">` blocks
2. Merge into a single @graph array:
   ```json
   {
     "@context": "https://schema.org",
     "@graph": [
       { "@type": "Organization", "@id": ".../#org", ... },
       { "@type": "BreadcrumbList", ... },
       { "@type": "FAQPage", ... }
     ]
   }
   ```
3. Add @id to entities that are referenced elsewhere
4. Remove all individual script tags, replace with single consolidated one

### AP-W07: Static Assets Blocking → Update robots.txt
**Type:** Auto-fixable

**Recipe:**
1. Add framework-specific static asset paths to robots.txt default rules:
   ```
   User-agent: *
   Disallow: /_next/static/
   Disallow: /_nuxt/
   Disallow: /_astro/
   Disallow: /static/chunks/
   ```
2. This saves crawl budget without affecting content visibility

### AP-W08: Missing OG Image
**Type:** Auto-fixable

**Recipe:**
1. Add og:image meta tag to all public pages
2. Recommended size: 1200x630px
3. Can be a default brand image if page-specific images aren't available

---

## Info Fixes

### AP-I01: Descriptive H2 → Question-Based H2
**Type:** Guided

**Recipe:**
Transform: "Marketing Landscape" → "Why Is AI Critical for B2B Marketing in 2026?"
Pattern: [Question word] + [specific topic] + [qualifier]?

### AP-I02: Pronouns → Explicit Brand Name
**Type:** Guided

**Recipe:** Replace "we", "our", "it", "this" with the actual brand/product name. AI may not resolve pronoun referents correctly.

### AP-I03: Missing dateModified
**Type:** Auto-fixable

**Recipe:**
1. Add `dateModified` to Article/Product schema
2. Display "Last Updated: [date]" visibly on the page
3. Use actual modification dates, not static values

### AP-I04: Missing sitemap.xml
**Type:** Guided

**Recipe:**
1. Generate sitemap.xml including all public pages
2. Reference it in robots.txt: `Sitemap: https://example.com/sitemap.xml`
3. For dynamic sites, use framework-specific sitemap generation
