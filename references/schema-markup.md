# Schema Markup Implementation Guide

## Table of Contents
1. [Why Schema Matters for GEO](#why-schema-matters-for-geo)
2. [Implementation Format: JSON-LD Required](#implementation-format-json-ld-required)
3. [Tier 1: Required (All Pages)](#tier-1-required-all-pages)
4. [Tier 2: By Page Type](#tier-2-by-page-type)
5. [Tier 3: Enhancement](#tier-3-enhancement)
6. [@graph Pattern — Consolidated Schemas](#graph-pattern--consolidated-schemas)
7. [@id Cross-References](#id-cross-references)
8. [Builder Function Pattern](#builder-function-pattern)
9. [Service vs Product Selection](#service-vs-product-selection)
10. [Dynamic Data in Schema](#dynamic-data-in-schema)
11. [Validation Tools](#validation-tools)
12. [Common Mistakes](#common-mistakes)

---

## Why Schema Matters for GEO

Schema markup is a translation layer that explicitly communicates content meaning to AI systems. Instead of AI "guessing" meaning through NLP, schema directly tells it what is a product, who is an author, and which questions are being answered.

Key data:
- Content with proper schema is **~2.5x more likely** to appear in AI-generated answers (Stackmatix, 2026)
- Schema-enhanced pages record **~30% higher click-through rates** vs standard results (BrightEdge)
- Google AI Overviews **explicitly reads structured data** when composing AI Overview responses

## Implementation Format: JSON-LD Required

**JSON-LD is the only practical choice.** It's separated from HTML content, allowing AI crawlers to extract structured signals without parsing conflicts. Microdata and RDFa embed schema inside HTML tags, which can cause parsing issues — avoid them.

---

## Tier 1: Required (All Pages)

### Organization — Company Identity

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "[Company Name]",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "description": "[1–2 sentence company description]",
  "sameAs": [
    "https://www.linkedin.com/company/[company]",
    "https://twitter.com/[company]"
  ],
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+1-XXX-XXX-XXXX",
    "contactType": "customer service",
    "availableLanguage": ["English"]
  }
}
```

### BreadcrumbList — Site Structure

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://example.com"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "[Category]",
      "item": "https://example.com/[category]"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "[Current Page]",
      "item": "https://example.com/[category]/[page]"
    }
  ]
}
```

---

## Tier 2: By Page Type

### FAQPage — Any Page with FAQ Section

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "[Question text]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[Answer text — 40–80 words, self-contained]"
      }
    }
  ]
}
```

### Article — Blog, Guide, Content Pages

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[H1 title]",
  "author": {
    "@type": "Person",
    "name": "[Author name]",
    "url": "[Author profile URL]",
    "jobTitle": "[Job title]"
  },
  "publisher": {
    "@type": "Organization",
    "name": "[Company name]",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/logo.png"
    }
  },
  "datePublished": "2026-03-24",
  "dateModified": "2026-03-24",
  "description": "[1–2 sentence meta description]",
  "mainEntityOfPage": "https://example.com/[page-url]"
}
```

### Product — Product/Service Pages

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "[Product name]",
  "description": "[1–2 sentence product description]",
  "brand": {
    "@type": "Brand",
    "name": "[Brand name]"
  },
  "offers": {
    "@type": "AggregateOffer",
    "lowPrice": "[Lowest price]",
    "highPrice": "[Highest price]",
    "priceCurrency": "USD",
    "offerCount": "[Number of plans]"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "[Rating]",
    "reviewCount": "[Review count]"
  }
}
```

### HowTo — Guide/Tutorial Pages

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "[Guide title]",
  "description": "[Guide summary]",
  "step": [
    {
      "@type": "HowToStep",
      "name": "[Step title]",
      "text": "[Step description]"
    }
  ]
}
```

### Service — SaaS/Service Businesses

```json
{
  "@context": "https://schema.org",
  "@type": "Service",
  "serviceType": "[Service type]",
  "provider": {
    "@type": "Organization",
    "name": "[Company name]"
  },
  "areaServed": "[Service area]",
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "[Catalog name]",
    "itemListElement": [
      {
        "@type": "Offer",
        "itemOffered": {
          "@type": "Service",
          "name": "[Plan name]"
        },
        "price": "[Price]",
        "priceCurrency": "USD"
      }
    ]
  }
}
```

---

## Tier 3: Enhancement

- **Person** — Author pages, team pages. Strengthens AI's E-E-A-T evaluation.
- **Review / AggregateRating** — Product/service pages. Used in AI's credibility assessment.
- **SiteLinksSearchBox** — Strengthens brand entity in AI knowledge graphs.
- **Speakable** — Identifies content for voice AI assistants.
- **VideoObject / ImageObject** — Multimodal search support.

---

## @graph Pattern — Consolidated Schemas

Multiple schemas on one page should be consolidated into a single `<script type="application/ld+json">` block using the `@graph` array. This ensures AI systems can parse all entities in one pass and link related entities together, rather than treating them as isolated fragments.

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://example.com/#org",
      "name": "[Company Name]",
      "url": "https://example.com",
      "logo": "https://example.com/logo.png",
      "sameAs": ["https://linkedin.com/company/..."]
    },
    {
      "@type": "WebSite",
      "@id": "https://example.com/#website",
      "url": "https://example.com",
      "name": "[Site Name]",
      "publisher": { "@id": "https://example.com/#org" }
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [...]
    },
    {
      "@type": "FAQPage",
      "mainEntity": [...]
    }
  ]
}
```

**Benefits:** Single parse for AI crawlers, entities linked via `@id` references, and easier to maintain than multiple separate script blocks.

---

## @id Cross-References

The `@id` property creates a unique identifier for an entity, allowing other entities to reference it without duplicating data. This builds a connected knowledge graph that AI systems can traverse.

How entities reference each other:
- **Organization** gets `"@id": "https://example.com/#org"`
- **WebSite** references its publisher via `"publisher": {"@id": "https://example.com/#org"}`
- **Article** references its author via `"author": {"@id": "https://example.com/#author-name"}`
- **WebPage** references the parent site via `"isPartOf": {"@id": "https://example.com/#website"}`

### Practical Example — Full Cross-Linked Graph

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://example.com/#org",
      "name": "Example Corp",
      "url": "https://example.com",
      "logo": "https://example.com/logo.png"
    },
    {
      "@type": "WebSite",
      "@id": "https://example.com/#website",
      "url": "https://example.com",
      "name": "Example Corp",
      "publisher": { "@id": "https://example.com/#org" }
    },
    {
      "@type": "WebPage",
      "@id": "https://example.com/blog/geo-guide",
      "url": "https://example.com/blog/geo-guide",
      "name": "Complete GEO Guide",
      "isPartOf": { "@id": "https://example.com/#website" }
    },
    {
      "@type": "Article",
      "headline": "Complete GEO Guide",
      "mainEntityOfPage": { "@id": "https://example.com/blog/geo-guide" },
      "author": { "@id": "https://example.com/#author-jane" },
      "publisher": { "@id": "https://example.com/#org" },
      "datePublished": "2026-03-24"
    },
    {
      "@type": "Person",
      "@id": "https://example.com/#author-jane",
      "name": "Jane Smith",
      "jobTitle": "Head of Content",
      "url": "https://example.com/team/jane-smith"
    }
  ]
}
```

---

## Builder Function Pattern

Instead of hardcoding JSON-LD in every page, use a utility function to generate schemas programmatically. This ensures brand information stays consistent and updates propagate automatically.

```typescript
// lib/schema.ts
const SITE_URL = 'https://example.com';
const ORG_ID = `${SITE_URL}/#org`;

export function buildOrganization() {
  return {
    '@type': 'Organization',
    '@id': ORG_ID,
    name: '[Brand]',
    url: SITE_URL,
    logo: `${SITE_URL}/logo.png`,
    sameAs: ['https://linkedin.com/company/...'],
  };
}

export function buildBreadcrumb(items: {name: string; url: string}[]) {
  return {
    '@type': 'BreadcrumbList',
    itemListElement: items.map((item, i) => ({
      '@type': 'ListItem',
      position: i + 1,
      name: item.name,
      item: item.url,
    })),
  };
}

export function buildPageSchema(pageSchema: object, breadcrumbs: {name: string; url: string}[]) {
  return {
    '@context': 'https://schema.org',
    '@graph': [
      buildOrganization(),
      buildBreadcrumb(breadcrumbs),
      pageSchema,
    ],
  };
}
```

**Benefits:** Single source of truth for brand information — update once and it applies everywhere. Eliminates copy-paste drift across pages.

---

## Service vs Product Selection

| Criteria | Use Product | Use Service |
|----------|------------|-------------|
| Tangible deliverable (physical/digital product) | Yes | |
| Ongoing capability/access (SaaS, consulting) | | Yes |
| One-time purchase | Yes | |
| Subscription/recurring | | Yes (with `hasOfferCatalog`) |
| E-commerce item | Yes | |
| Professional services | | Yes |

**Note:** Many SaaS companies incorrectly use `Product`. `Service` + `hasOfferCatalog` is more semantically accurate for subscription-based offerings.

---

## Dynamic Data in Schema

Never hardcode prices, ratings, or other frequently changing data in JSON-LD. Pull from your database or CMS to keep schema in sync with reality.

```typescript
// Example: Dynamic pricing and ratings
export async function buildProductSchema(productId: string) {
  const product = await db.product.findUnique({ where: { id: productId } });
  const reviews = await db.review.aggregate({ where: { productId } });
  
  return {
    '@type': 'Product',
    name: product.name,
    description: product.description,
    offers: {
      '@type': 'AggregateOffer',
      lowPrice: product.plans[0].price,
      highPrice: product.plans.at(-1).price,
      priceCurrency: product.currency,
      offerCount: product.plans.length,
    },
    aggregateRating: reviews._count > 0 ? {
      '@type': 'AggregateRating',
      ratingValue: reviews._avg.rating,
      reviewCount: reviews._count,
    } : undefined,
  };
}
```

**Key point:** Hardcoded prices or ratings will drift out of sync with your actual data, which AI systems may flag as a content-schema mismatch.

---

## Validation Tools

1. **Google Rich Results Test** — Verify structured data is properly recognized
2. **Schema Markup Validator** — Check syntax errors, missing fields, incorrect nesting
3. **Google Search Console > Enhancements** — Monitor actual indexing status

---

## Common Mistakes

| Mistake | Impact |
|---------|--------|
| Wrong schema type | Confuses AI systems |
| Missing required fields | Causes errors |
| Content–schema mismatch | May be flagged as deceptive |
| Duplicate schemas | Parsing issues |
| Stale data (no updates) | AI uses freshness as trust signal — regularly update prices, dates, and variable information |
| Separate JSON-LD blocks | AI may not link related entities — use @graph |
| Missing @id references | Entities appear isolated instead of connected |
| Hardcoded brand info | Update one page, forget nine others — use builder function |
| Product schema for SaaS | Service + hasOfferCatalog is more accurate |
