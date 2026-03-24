# Page Type Templates & Checklists

## Table of Contents
1. [Evergreen Pages (Product/Service)](#1-evergreen-pages-productservice)
2. [Blog / Content Marketing Pages](#2-blog--content-marketing-pages)
3. [Landing Pages](#3-landing-pages)
4. [FAQ Pages](#4-faq-pages)
5. [Pillar / Category Hub Pages](#5-pillar--category-hub-pages)
6. [Before/After Refactoring Examples](#6-beforeafter-refactoring-examples)

---

## 1. Evergreen Pages (Product/Service)

### Structure Template

```
[H1] [Product/Service Name] — [Core value proposition as query-matching or definitional title]

[TL;DR / Key Takeaways] — 3–5 line summary, above the fold

[H2] What is [Product/Service]?
→ First 2 sentences: clear definition (independently citable)
→ Key features summary
→ Who it's for

[H2] Key Features
→ Each feature as H3
→ Under each H3: 1-sentence feature definition + specific numbers/results + use scenario

[H2] [Product/Service] vs [Competing Category/Alternatives]
→ Comparison table (features, pricing, target audience, etc.)
→ Differentiation described with fact-based statements

[H2] Pricing
→ Pricing table with actual numbers ("Contact us" pages get skipped by AI)
→ Features included per plan

[H2] Customer Case Studies / Results
→ Cases with specific numbers (X% increase, Y hours saved, etc.)

[H2] FAQ
→ 5–10 questions, each answer 40–80 words
→ FAQPage schema applied

[Schema Markup: Product, Organization, FAQPage, AggregateRating]
```

### Checklist

- [ ] H1 contains the core search query/phrase
- [ ] First 200 words function as a standalone answer
- [ ] TL;DR section is above the fold
- [ ] Pricing shows actual numbers (not just "contact us")
- [ ] At least 1 comparison table exists
- [ ] FAQ section has FAQPage schema applied
- [ ] Product and Organization schemas are implemented
- [ ] Brand name is used explicitly instead of pronouns
- [ ] Each section answers only one question
- [ ] Specific numbers appear every 150–200 words
- [ ] "Last Updated" date is displayed

---

## 2. Blog / Content Marketing Pages

### Structure Template

```
[H1] [Question-based title — exactly matching target prompt]

[Author Byline] — Name, title, credentials, external links
[Published Date] [Last Modified Date]

[TL;DR / Key Takeaways]
→ 3–5 key insights, each a citable single sentence

[Table of Contents] — with descriptive anchor links

[H2] [Topic Question 1]?
→ Citation Block: first 2–3 sentences directly answer the question
→ Supporting data/statistics
→ Specific example or case study

[H2] [Topic Question 2]?
→ Same pattern
→ Include comparison tables, process explanations, etc.

[H2] [Topic Question N]?
→ ...

[H2] Conclusion / Key Takeaways
→ Summarize the most important insight in one sentence

[H2] FAQ
→ 5–8 questions not covered in the main body

[Schema Markup: Article, Person, FAQPage, BreadcrumbList]
```

### Checklist

- [ ] H1 matches a prompt users would actually type into AI
- [ ] Author byline has name, credentials, external profile links
- [ ] Both published and last modified dates are displayed
- [ ] TL;DR section is above the fold
- [ ] Table of contents has descriptive anchor links
- [ ] All H2s are in question form
- [ ] First 2–3 sentences under each H2 function as standalone answers
- [ ] All key terms have explicit definitions
- [ ] Specific numbers/statistics every 150–200 words
- [ ] At least 1 comparison table or framework
- [ ] External authoritative source citations included
- [ ] Article, Person, FAQPage schemas applied
- [ ] Key insights distilled into quotable one-liner summaries

---

## 3. Landing Pages

### Structure Template

```
[H1] [Core value proposition — including target query]

[Hero Section]
→ First 40–60 words: clearly define what this product/service is and who it's for
→ 1–2 key numbers (e.g., "Used by 10,000+ companies", "Average 40% conversion lift")

[H2] What Problem Does It Solve?
→ Target customer's pain points explicitly stated
→ Solution summarized in 2–3 sentences

[H2] Key Features / How It Works
→ Each feature as H3
→ Feature description + result numbers

[H2] Competitive Comparison / Differentiators
→ Comparison table (vs category alternatives)

[H2] Customer Testimonials / Case Studies
→ Testimonials with name, title, and company
→ Quantified results

[H2] Pricing
→ Actual numbers included

[H2] FAQ
→ 5–10 purchase-decision questions

[CTA]

[Schema Markup: Product/Service, Organization, FAQPage, Review/AggregateRating]
```

### Checklist

- [ ] Hero section's first sentence clearly defines the service
- [ ] Real pricing exists (not just "contact us")
- [ ] Comparison table is present
- [ ] Testimonials include specific numbers
- [ ] FAQ contains purchase-decision information
- [ ] Product/Service, Organization, FAQPage schemas applied

---

## 4. FAQ Pages

FAQ pages deliver the fastest GEO wins. Frase.io recommends starting GEO implementation with FAQ optimization.

### Structure Template

```
[H1] Frequently Asked Questions About [Topic]

[H2] [Question 1]?
→ First sentence: direct answer within 40–60 words (AI extraction target)
→ 2–3 supplementary sentences

[H2] [Question 2]?
→ Same pattern

...repeat...

[Schema Markup: FAQPage (required), BreadcrumbList]
```

### Checklist

- [ ] Covers the 10–15 most common industry questions
- [ ] Each answer's first sentence is independently complete
- [ ] FAQPage schema applied to all Q&A pairs
- [ ] Questions match actual user prompts
- [ ] Answers contain specific information, not vague language

---

## 5. Pillar / Category Hub Pages

### Structure Template

```
[H1] Complete Guide to [Category]: Everything You Need to Know

[TL;DR] — 3–5 sentence summary of this guide

[Table of Contents] — links to all subtopics

[H2] What is [Category]?
→ Clear definition (citable format)

[H2] [Subtopic 1]
→ Core explanation + internal link to detailed content page

[H2] [Subtopic 2]
→ Same pattern

[H2] [Category] Comparison: [A] vs [B] vs [C]
→ Comprehensive comparison table

[H2] FAQ

[Schema Markup: Article, BreadcrumbList, FAQPage, ItemList (optional)]
```

Per Writesonic research, category hubs maintain stable citation rates across industries, with financial services showing the highest rates at 13–23%.

---

## 6. Before/After Refactoring Examples

### Example 1: Evergreen Page Opening

**Before:**
```
The digital marketing landscape is rapidly changing.
Companies demand ever-higher marketing ROI,
and at the center of this change, we offer innovative solutions.
Get started today.
```
Problem: Focused on hooks and mood-setting. No extractable facts. "Innovative solutions" is undefined.

**After:**
```
[BrandName] is an AI-powered marketing automation platform for B2B SaaS companies.
It manages email campaign automation, lead scoring, and funnel analysis
from a single dashboard, with a track record of improving
client conversion rates by an average of 34%.
Starting at $99/month with a 14-day free trial.
```
Improvement: First sentence is a clear definition. Brand name explicit. Specific numbers. Pricing included. AI can extract immediately.

### Example 2: Blog H2 Heading

**Before:**
```
## Changes in the Marketing Landscape
Recently, the marketing landscape has changed a lot. Various trends are...
```
Problem: Vague heading. First sentence is situational description, not an answer.

**After:**
```
## Why Is AI Automation Critical for B2B Marketing in 2026?
AI automation is critical for B2B marketing because it delivers
an average 3.2x higher lead conversion rate compared to manual campaigns
(Forrester, 2025). Lead scoring, personalized email, and
predictive analytics show the greatest impact.
```
Improvement: Question-form H2. First sentence directly answers. Specific numbers with source. Independently citable.

### Example 3: FAQ Answer

**Before:**
```
Q: What are your prices?
A: Pricing varies depending on several factors.
   Please contact our sales team for details.
```
Problem: No extractable information. "Contact us" gets skipped by AI.

**After:**
```
Q: What is [BrandName]'s pricing?
A: [BrandName] offers 3 plans:
   Starter ($49/mo, 3 users), Pro ($149/mo, 10 users),
   and Enterprise (custom quote, unlimited users).
   All plans include a 14-day free trial,
   with 20% discount on annual billing.
```
Improvement: Brand name in question. Specific pricing. Plan differences explicit. AI can use for price comparisons.

### Example 4: Brand Entity Expression

**Before:**
```
Our solution is easy to use and powerful.
Through it, you can significantly improve your business results.
```
Problem: "Our", "it" — AI may not accurately identify pronoun referents.

**After:**
```
The [BrandName] marketing automation platform features a drag-and-drop interface
that lets non-developers set up campaigns in under 30 minutes.
Over 200 [BrandName] clients achieved a 23% reduction
in marketing costs within 6 months of adoption.
```
Improvement: Brand name explicitly repeated. Specific usability description. Quantified results.
