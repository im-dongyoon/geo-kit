# Content Signal Stack — Universal Minimum

> When to read this: Before building or auditing any page. These 5 signals are the floor — every page must have them, regardless of purpose type (Content, Standing, or Logic).

## The 5 Universal Signals

These signals were identified from 17 production GEO optimization changes. Every successful optimization included all 5.

### 1. BreadcrumbList Schema
Every page needs a BreadcrumbList to signal its position in the site hierarchy. AI uses this to understand site structure and navigate between related pages.

**Applies to all purposes:** Content, Standing, Logic (user-facing pages)

### 2. H1 Optimization
Single H1 per page containing the page's core concept. No duplicate H1s (common in responsive designs with separate mobile/desktop headers).

**Applies to all purposes.** For Logic pages without user-facing content, this may not apply.

### 3. Clean Opening
First 40-60 words must clearly state what the page is about. This is the AI extraction target — the snippet most likely to appear in AI-generated answers.

**How it adapts by purpose:**
| Purpose | Clean Opening Goal | Example |
|---------|-------------------|---------|
| Content | Answer the core question | "[Topic] is [definition]. It works by [mechanism], delivering [result]." |
| Standing | Define the entity/product | "[Brand] is a [category] for [target]. It provides [key capabilities] starting at [price]." |
| Logic | Document the endpoint | "This API endpoint returns [data type] for [use case]. Authentication required." |

### 4. FAQ Section + FAQPage Schema
Every page benefits from a FAQ section. FAQPage schema is the fastest GEO win (Frase.io). The question types differ by purpose.

**How it adapts by purpose:**
| Purpose | FAQ Question Types | Example Questions |
|---------|-------------------|-------------------|
| Content | Topic-related questions | "What is GEO?", "How does AI citation work?" |
| Standing | Purchase/decision questions | "What's the pricing?", "How does [Brand] compare to [Competitor]?" |
| Logic | Integration/usage questions | "How do I authenticate?", "What are the rate limits?" |

### 5. JSON-LD @graph
All schemas on a page should be consolidated into a single `<script type="application/ld+json">` tag using the @graph array pattern. This ensures AI can link related entities (Organization → WebPage → Author).

**Minimum @graph for any page:**
```json
{
  "@context": "https://schema.org",
  "@graph": [
    { "@type": "Organization", "@id": "https://example.com/#org", "..." },
    { "@type": "BreadcrumbList", "..." },
    // + page-type-specific schema (Article, Product, Service, FAQPage, etc.)
  ]
}
```

See `schema-markup.md` for complete @graph templates and @id cross-reference patterns.

## Checklist

- [ ] BreadcrumbList schema present
- [ ] Single H1 containing core concept
- [ ] First 40-60 words state what the page is about
- [ ] FAQ section with FAQPage schema
- [ ] All schemas in single @graph array

## Relationship to Purpose-Specific Criteria

These 5 signals are the FLOOR. Purpose-specific criteria (from `citation-checklist.md`) add ON TOP:
- Content adds: author byline, fact density, topical completeness, etc.
- Standing adds: pricing visibility, comparison tables, entity clarity, etc.
- Logic adds: SSR verification, clean URLs, crawl budget optimization, etc.
