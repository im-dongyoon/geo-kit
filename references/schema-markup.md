# Schema Markup Implementation Guide

## Table of Contents
1. [Why Schema Matters for GEO](#why-schema-matters-for-geo)
2. [Implementation Format: JSON-LD Required](#implementation-format-json-ld-required)
3. [Tier 1: Required (All Pages)](#tier-1-required-all-pages)
4. [Tier 2: By Page Type](#tier-2-by-page-type)
5. [Tier 3: Enhancement](#tier-3-enhancement)
6. [Validation Tools](#validation-tools)
7. [Common Mistakes](#common-mistakes)

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
