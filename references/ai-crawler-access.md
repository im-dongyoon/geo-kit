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
