# Platform-Specific Optimization Strategies & Measurement

## Table of Contents
1. [Per-Platform Strategies](#per-platform-strategies)
2. [Universal Strategy](#universal-strategy)
3. [GEO KPIs](#geo-kpis)
4. [Monitoring Process](#monitoring-process)

---

## Per-Platform Strategies

AI platforms have different citation patterns. Apply universal principles first, then layer platform-specific optimizations.

### ChatGPT

- Prefers **encyclopedic, comprehensive content**.
- GPT-5.4 now references actual brand websites in **56% of citations** (vs 8% in GPT-5.3).
- GPT-5.4 **reads pricing pages directly** — "contact us" pages with no real numbers get skipped.
- Performs multi-phase research using domain-restricted queries and `site:` operators.

### Perplexity

- Highly values **recency** and community references.
- **Always provides source citations** with answers, creating referral traffic opportunities.
- Recognizes authority from content with **comprehensive citations and references**.

### Google AI Overviews

- **Prioritizes content with high organic rankings** — existing SEO matters.
- **Explicitly reads structured data** (Schema Markup) when composing AI Overview responses.
- Content holding **Featured Snippets** gets priority in AI Overview inclusion.
- However, this advantage is declining: AI Overview citations from top 10 dropped from 76% to 38% (Ahrefs, 2026).

### Claude

- Generates answers with source citations, but public documentation on citation patterns remains limited.
- General principles apply: strong **E-E-A-T signals** and well-structured content are preferred.

---

## Universal Strategy (All Platforms)

- Clear hierarchy (H1 → H2 → H3) for extractable information
- Include **both** encyclopedic definitions (for ChatGPT) **and** practical examples (for Perplexity)
- Maintain **both** schema markup (for Google AI) **and** conversational readability (for Perplexity)
- **Quarterly updates** to satisfy Perplexity's recency preference

---

## GEO KPIs

Traditional SEO metrics (rank, clicks, bounce rate) alone cannot capture GEO performance. Add these:

| KPI | Description | Measurement Method |
|-----|-------------|-------------------|
| AI Citation Rate | How often your brand/content is cited in AI answers | Writesonic, Profound, Semrush Enterprise AIO, etc. |
| AI Visibility Score | % of target prompts where your brand appears | Manual prompt testing + GEO tracking tools |
| Share of Voice | Brand presence in AI answers vs competitors | GEO analytics platforms |
| Citation Sentiment | Whether AI presents your brand positively/neutrally/negatively | Sentiment analysis tools |
| AI Referral Traffic | Visits and conversions from AI search | GA4 referral source analysis |
| Content Extraction Rate | How often your content is extracted by AI | Log file analysis |

---

## Monitoring Process

### Monthly Prompt Testing

1. List 10–15 core questions your brand targets
2. Enter each question into ChatGPT, Perplexity, Gemini, and Claude
3. Record: brand mention (yes/no), cited source, competitor presence, sentiment
4. Identify **"citation gaps"** — topics where competitors are cited but you aren't
5. Refactor content for gap topics following GEO guidelines

### GA4 AI Traffic Tracking

Segment AI platform referral sources in GA4. Analyze traffic volume and behavior from OpenAI, Perplexity, Google (AI Overviews), and other AI platforms separately.

### AI Crawler Log Analysis

Monitor server logs for AI bot access patterns. Identify which pages get crawled and which get ignored to prioritize optimization efforts.
