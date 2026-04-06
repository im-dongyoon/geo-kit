# AI Crawler Access Management

## Table of Contents
1. [Understanding the 3-Layer Crawler Architecture](#understanding-the-3-layer-crawler-architecture)
2. [Recommended robots.txt Configuration](#recommended-robotstxt-configuration)
3. [Important Caveats](#important-caveats)

---

## Understanding the 3-Layer Crawler Architecture

As of 2026, major AI companies operate crawlers separated by purpose:

| Company | Training | Search Indexing | User Retrieval |
|---------|----------|-----------------|----------------|
| OpenAI | GPTBot | OAI-SearchBot | ChatGPT-User |
| Anthropic | ClaudeBot | Claude-SearchBot | Claude-User |
| Perplexity | — | PerplexityBot | Perplexity-User |
| Google | Google-Extended | Googlebot | — |

**Key points:**
- Blocking a training bot does **not** block the search bot.
- Blocking a search bot **removes you from that AI platform's search results**.
- Anthropic states that blocking Claude-SearchBot **"may reduce"** visibility.
- OpenAI states more directly that blocking OAI-SearchBot means you **"will not appear"** in ChatGPT search answers.

---

## Recommended robots.txt Configuration

**Strategy: Allow AI search bots + Block training bots**

```
# ===================================
# robots.txt — GEO Optimized
# Last Updated: 2026-03-24
# Strategy: Maximize AI search citation + Protect training data
# ===================================

# Traditional search engines — Allow
User-agent: Googlebot
Allow: /

User-agent: Bingbot
Allow: /

# AI search/retrieval bots — Allow (for citation)
User-agent: OAI-SearchBot
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: Claude-SearchBot
Allow: /

User-agent: Claude-User
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Perplexity-User
Allow: /

User-agent: Amazonbot
Allow: /

# AI training bots — Block (content protection)
User-agent: GPTBot
Disallow: /

User-agent: ClaudeBot
Disallow: /

User-agent: Google-Extended
Disallow: /

User-agent: CCBot
Disallow: /

User-agent: Bytespider
Disallow: /

User-agent: Meta-ExternalAgent
Disallow: /

User-agent: Applebot-Extended
Disallow: /

User-agent: Diffbot
Disallow: /

# Default rules
User-agent: *
Disallow: /admin/
Disallow: /api/
Disallow: /internal/

Sitemap: https://[yourdomain].com/sitemap.xml
```

---

## Important Caveats

### Quarterly Review Required
AI companies frequently launch new crawlers. Anthropic consolidated its previous `anthropic-ai` and `Claude-Web` bots into `ClaudeBot` — sites that didn't update were left unprotected against the new bot. Review your robots.txt quarterly.

### Cloudflare Users: Caution
Cloudflare's "Block AI bots" toggle blocks **both** training and search bots. WAF rules apply **before** robots.txt, so individual crawler settings (AI Crawl Control) must be used instead.

### Perplexity Exception
There are reports that `Perplexity-User` generally **does not respect robots.txt**. Blocking `PerplexityBot` may not fully prevent Perplexity from serving your content.

### Server Log Monitoring
Verify which AI bots actually visit your site. Use commands like:
```bash
grep -Ei "gptbot|claudebot|perplexitybot|oai-searchbot" access.log
```
to check crawl activity and prioritize optimization for bots that actually visit.

---

## Framework Static Asset Blocking

AI crawlers waste budget crawling CSS, JS, and image files. Block framework-specific static asset paths in robots.txt.

Add these lines to the default `User-agent: *` section of robots.txt:

```
# Framework static assets — save crawl budget
# Next.js
Disallow: /_next/static/
Disallow: /_next/image/

# Nuxt
Disallow: /_nuxt/

# Astro  
Disallow: /_astro/

# General
Disallow: /static/chunks/
Disallow: /assets/
```

**Note:** Only block paths that serve compiled assets (CSS/JS bundles), not paths that serve content. Check your framework's build output to confirm paths.

---

## llms.txt — AI-Specific Site Description

`llms.txt` is an emerging convention (proposed by llmstxt.org) for providing AI systems a concise, machine-readable summary of your site. While not universally adopted yet, early support from Anthropic (Claude) and others makes it worth implementing.

### Format

Place at site root: `https://example.com/llms.txt`

```
# [Site Name]

> [One-line description of the site]

## About
[2-3 sentences describing what the site/company does, who it serves, key offerings]

## Key Pages
- [Page Title](https://example.com/page): [Brief description]
- [Page Title](https://example.com/page): [Brief description]

## Contact
- Website: https://example.com
- Email: contact@example.com
```

### Optional: llms-full.txt

For comprehensive AI context, provide `llms-full.txt` with more detailed information:
- Full product/service descriptions
- Pricing details
- Technical specifications
- FAQ content

### Implementation

1. Create `llms.txt` at the site root (static file or generated route)
2. Optionally create `llms-full.txt` for comprehensive detail
3. Reference in `<head>`:
   ```html
   <link rel="llms" href="/llms.txt" />
   ```
4. Keep content current — update when major site changes occur

---

## noindex Strategy

Not every page should be visible to AI. Proper noindex management prevents crawl budget waste and keeps AI focused on valuable content.

### Pages That Should Have noindex

| Category | Examples | Why |
|----------|----------|-----|
| Authentication | /login, /signup, /reset-password | No GEO value, private flow |
| Dashboard/App | /dashboard/*, /settings/* | User-specific, behind auth |
| Admin | /admin/* | Internal only |
| Checkout/Order | /checkout, /order/*, /cart | Transactional, no citation value |
| Legal boilerplate | /terms, /privacy (unless SEO-targeted) | Low citation value |
| Utility | /404, /500, /maintenance | Error pages |
| API routes | /api/* (already in default robots.txt) | Data endpoints |

### Pages That Should NOT Have noindex

| Category | Examples | Why |
|----------|----------|-----|
| Product/Service | /product/*, /pricing, /features | Core GEO targets |
| Content | /blog/*, /guides/*, /docs/* | Citation targets |
| Company | /about, /team, /careers | Entity signals |
| Landing pages | /, /solutions/* | Recommendation targets |

### Implementation Pattern

For Next.js App Router:
```typescript
// app/(private)/layout.tsx — covers all private routes
export const metadata = {
  robots: { index: false, follow: false },
};
```

For other frameworks, apply noindex via meta tags or response headers for private route groups.
