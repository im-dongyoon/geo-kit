# GEO Citation Readiness Checklist

Run through this checklist before publishing or auditing any page. Apply the **Universal** section to all pages, then add the section matching the page's purpose (Content, Standing, or Logic).

Based on Writesonic's Citation Readiness framework, enhanced with purpose-specific criteria from production GEO optimization experience.

---

## Universal Checklist (All Pages)

These 12 items apply regardless of page purpose. Items 1-5 are the Content Signal Stack minimum.

### Content Signal Stack (5 items)

- [ ] 1. BreadcrumbList schema present with correct site hierarchy
- [ ] 2. Single H1 per page containing the core concept/query
- [ ] 3. First 40-60 words clearly state what the page is about (Clean Opening)
- [ ] 4. FAQ section present with FAQPage schema applied
- [ ] 5. All schemas consolidated in a single JSON-LD @graph array

### Technical Accessibility (7 items)

- [ ] 6. robots.txt allows AI search bots (OAI-SearchBot, Claude-SearchBot, PerplexityBot)
- [ ] 7. Cloudflare WAF is not blocking AI search bots
- [ ] 8. sitemap.xml is up to date and includes all important pages
- [ ] 9. Valid HTML structure present (DOCTYPE, `<html>`, `<head>`, `<body>`)
- [ ] 10. Language declaration (`lang` attribute on `<html>` element)
- [ ] 11. Viewport meta tag present (`<meta name="viewport">`)
- [ ] 12. Page load speed is satisfactory (indirect impact on crawler accessibility)

---

## Content Purpose (+12 items)

For pages where the goal is **AI citation** — blog posts, guides, documentation, articles.

### Opening & Structure (3 items)

- [ ] 13. First 200 words function as an independent citation (complete answer when read alone)
- [ ] 14. Table of contents with descriptive anchor links is present
- [ ] 15. Key Takeaways / TL;DR section is above the fold

### Topical Completeness (3 items)

- [ ] 16. All major subtopics covered (check competitor H2s for gaps)
- [ ] 17. Each section answers only one specific question (atomic fact structure)
- [ ] 18. Specific numbers, statistics, and data points included (no vague "significant increase")

### Extraction Quality (3 items)

- [ ] 19. H2 headings are in question form matching actual user prompts
- [ ] 20. Paragraphs kept to 2-4 sentences (optimal: 50-200 characters per paragraph)
- [ ] 21. Terminology used consistently (same concept = same word throughout)

### Authorship & Trust (3 items)

- [ ] 22. Author byline with name, credentials, and external profile links present
- [ ] 23. Article and Person schemas implemented
- [ ] 24. Both published date and last modified date displayed

**Total for Content pages: 24 items** (12 universal + 12 content)

---

## Standing Purpose (+10 items)

For pages where the goal is **AI recommendation** — product pages, pricing, about, features, services.

### Entity Clarity (3 items)

- [ ] 13. Brand/product name used explicitly instead of pronouns ("we", "it", "this")
- [ ] 14. Product or Service definition in the first 40 words (what it is, who it's for)
- [ ] 15. Brand, product, and feature names consistent across all pages and platforms

### Recommendation Triggers (4 items)

- [ ] 16. Pricing shows real numbers (not just "contact us" — AI skips those)
- [ ] 17. At least 1 comparison table present (vs competitors or alternatives)
- [ ] 18. Customer testimonials or case studies with specific, quantified results
- [ ] 19. Product/Service and Organization schemas implemented (not Article)

### Discoverability (3 items)

- [ ] 20. OpenGraph tags complete (og:title, og:description, og:image, og:type)
- [ ] 21. Meta description (150-160 chars) includes core product/service definition
- [ ] 22. Title tag (50-60 chars) contains the target query

**Total for Standing pages: 22 items** (12 universal + 10 standing)

---

## Logic Purpose (+8 items)

For pages where the goal is **AI crawlability** — SSR routes, dynamic pages, API-adjacent content, data-driven pages.

### Server Rendering (3 items)

- [ ] 13. Initial HTML response contains complete page content (not CSR skeleton)
- [ ] 14. No Suspense/loading boundaries hiding primary content from crawlers
- [ ] 15. Dynamic routes pre-rendered via generateStaticParams or equivalent

### URL & Crawl Optimization (3 items)

- [ ] 16. Clean URL slugs used (not UUIDs or query-param-only navigation)
- [ ] 17. Framework static assets blocked in robots.txt (/_next/static/, etc.)
- [ ] 18. Non-public pages (dashboard, auth, admin) have noindex applied

### Data Accessibility (2 items)

- [ ] 19. Key content not hidden behind modals, tabs, or accordions
- [ ] 20. Proper 301 redirects in place for any migrated/changed URLs

**Total for Logic pages: 20 items** (12 universal + 8 logic)

---

## Cross-Purpose Items

Some items from one purpose checklist may be relevant to other purposes. Apply them when applicable:

- **Comparison tables** (Standing #17): Also valuable for Content pages with product/tool comparisons
- **Author byline** (Content #22): Also valuable for Standing pages with thought leadership content
- **SSR verification** (Logic #13): Also important for Standing/Content pages using dynamic data

---

## Distribution & Post-Publish (All Purposes)

These items apply after publishing, regardless of page purpose:

- [ ] Plan to share on LinkedIn and relevant communities within 48 hours
- [ ] Plan to secure at least 1 external backlink/mention
- [ ] Schedule for testing brand citation in target AI prompts exists
- [ ] Quarterly content update schedule (fresh data, new insights) is planned
