# GEO Core Principles & Content Structure Design

## Table of Contents
1. [7 Conditions for AI Citation](#7-conditions-for-ai-citation)
2. [Content Structure Design Principles](#content-structure-design-principles)

---

## 7 Conditions for AI Citation

Based on Writesonic's 31-Point Citation Readiness Checklist and analysis of hundreds of pages, content that consistently earns AI citations meets these 7 conditions.

### 1. Clean Opening Answer

- **The first 1–2 sentences are what AI extracts for citation.** If you open with hooks or provocative opinions, AI skips them.
- Place a direct answer to the core question within the first 40–60 words.
- The first 200 words must function as a standalone, complete answer. AI should be able to read just that portion and convey accurate information.

**Bad:**
```
The digital marketing landscape is rapidly changing.
Companies demand ever-higher marketing ROI,
and at the center of this change, we offer innovative solutions.
Get started today.
```

**Good:**
```
[BrandName] is an AI-powered marketing automation platform for B2B SaaS companies.
It manages email campaign automation, lead scoring, and funnel analysis
from a single dashboard, with a track record of improving
client conversion rates by an average of 34%.
Starting at $99/month with a 14-day free trial.
```

### 2. Topical Completeness

- Cover all major subtopics for the subject.
- Analyze competitor H2 headings to identify coverage gaps and fill them.
- Pages with "more complete answers" earn **8x more AI citations** (Otterly, 2026).

### 3. Visible Authorship & E-E-A-T

- Attach author profiles with name, credentials, and external links (LinkedIn, Crunchbase) to all content.
- Structure company/author pages with career history, specialization, and external certifications.
- AI uses "who wrote this" as a **primary trust signal**.

### 4. Crawler Accessibility

- 73% of websites technically block AI crawlers without knowing it.
- Explicitly allow GPTBot, ClaudeBot, PerplexityBot, and other AI search bots in robots.txt.
- See `ai-crawler-access.md` for detailed configuration.

### 5. Extraction-Friendly Structure

- Use **question-based H2 headings**. Example: "What is GEO?" (O) vs "Understanding the Environment" (X)
- Keep paragraphs to **2–4 sentences**. Long text blocks reduce clarity.
- Use terminology **consistently**. Expressing the same concept with multiple words confuses AI.
- Actively leverage **tables, comparison frameworks, and definition blocks**.

### 6. Distribution Beyond Your Site

- Share on LinkedIn and relevant communities **within 48 hours** of publishing.
- Secure at least **1 external backlink, citation, or mention**.
- Repurpose content into YouTube descriptions, LinkedIn carousels, short-form videos, etc. This gives AI more citation opportunities.

### 7. Post-Publish Iteration

- Regularly add fresh data, new insights, and **"Last Updated" timestamps**.
- AI uses **freshness signals** in trust evaluation.
- Track which prompts surface your brand and identify gaps where competitors are cited but you aren't.

---

## Content Structure Design Principles

### Design at the "Atomic Fact" Level

The core shift in GEO: **AI extracts individual paragraphs, not entire pages.** From a 3,000-word article, AI may cite just one 60-word paragraph and ignore the rest.

Therefore, each section must:
- Answer **one specific question** without mixing multiple topics
- Be **self-contained** — meaningful without surrounding context
- Distill key insights into a **quotable one-liner summary**

### Semantic Chunking

SEO prefers comprehensive long-form content. GEO requires the same comprehensive content to be **semantically chunked** — organizing information so AI can extract specific facts without surrounding context.

**How to execute:**
- Place the core answer in the **first 2–3 sentences** under each H2 (Citation Block pattern)
- Follow with context, evidence, and examples as supplementary material
- Include **explicit definitions** for every key term — don't assume the reader knows jargon

### Fact Density

- Insert specific numbers, statistics, or data points **every 150–200 words**
- Replace vague expressions like "significant increase" with concrete numbers
- Princeton GEO research found that **Statistics Addition** showed particularly high visibility gains in legal/government domains and opinion-based queries
- **Fluency Optimization** alone was confirmed to produce 15–30% visibility improvement

### Entity Clarity

- **Never replace brand names with pronouns** ("we", "it", "this")
- Bad: "This feature helps with GEO optimization"
- Good: "[BrandName] provides GEO optimization features"
- Maintain **consistent naming** for brands, products, and features across all platforms
- Structure entity relationships with Organization, Person, Product schemas

### The Power of Comparison Content

- Include at least **1 comparison table or framework** (vs competitors, before/after, X vs Y)
- Writesonic analysis: **listicle formats** consistently show high citation rates across industries. Gemini cites listicles 1.4x more than ChatGPT on average.
- **"Best [category] for [use case]"** style BOFU roundup content is a core format for AI citations
