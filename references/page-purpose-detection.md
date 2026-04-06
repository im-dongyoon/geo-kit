# Page Purpose Detection

> When to read this: During Step 0 of audit and build workflows when determining a page's GEO purpose.

## Three-Purpose Taxonomy

| Purpose | Goal | What AI Does | Example Pages |
|---------|------|-------------|---------------|
| **Content** | Citation | AI quotes/cites this page as a source | /blog/, /guides/, /docs/, /changelog/, .md/.mdx files |
| **Standing** | Recommendation | AI recommends this product/service/company | /pricing/, /about/, /product/, /features/, /team/, /careers/, /case-studies/ |
| **Logic** | Crawlability | AI can access and read the data | /api/, middleware, SSR routes, dynamic rendering, server actions |

**Content** pages aim for citation — AI pulls a quote or fact and attributes it. The GEO ceiling is determined by how quotable and structured the prose is. Structured data (Article, HowTo) and clear headings matter most.

**Standing** pages aim for recommendation — AI mentions your brand when a user asks "best X for Y." The GEO ceiling depends on trust signals, comparison-friendly data, and Organization/Product schema. Social proof and quantified claims matter most.

**Logic** pages aim for crawlability — AI must physically reach and parse the data. There is no citation or recommendation ceiling; the page either works or doesn't. Bot-friendly rendering, correct status codes, and clean response formats matter most.

## Detection Signal Priority

### Priority 1: GEO Spec Page Map (Highest Confidence)

If `geo-spec/page-map.md` exists and contains a matching path pattern, use that classification directly. No heuristics needed — the user has already declared intent.

### Priority 2: File Path Patterns (High Confidence)

| Purpose | Path Patterns |
|---------|---------------|
| Content | `/blog/`, `/posts/`, `/articles/`, `/guides/`, `/docs/`, `/changelog/`, `/content/`, `/writing/`, `.md`, `.mdx` |
| Standing | `/pricing/`, `/about/`, `/product/`, `/features/`, `/team/`, `/careers/`, `/contact/`, `/case-studies/`, `/testimonials/`, `/partners/`, `/`, `/home` |
| Logic | `/api/`, `/sitemap`, `/rss`, `/feed`, `middleware.*`, `_middleware.*`, `route.ts`, `route.js`, `+server.ts`, `+server.js` |

### Priority 3: Code Patterns (Medium Confidence)

**Content signals:**
- `author` field, `publishedAt` / `date` / `createdAt` fields
- MDX/markdown imports or CMS fetch calls
- Reading time calculation
- Article/BlogPosting schema already present

**Standing signals:**
- Pricing table/component, feature grid/list
- Team member arrays, testimonial components
- Hero section with CTA buttons
- Product/Service schema already present

**Logic signals:**
- `getServerSideProps`, `getStaticProps`, `loader`/`action` (Remix)
- API response handlers, `Response.json()`
- Dynamic route params with data fetching
- No existing schema (absence is a signal)
- Bot detection or user-agent checks

### Priority 4: Existing Schema Types (Hint)

| Purpose | Schema Types |
|---------|-------------|
| Content | Article, BlogPosting, NewsArticle, HowTo, TechArticle |
| Standing | Product, Service, Organization (standalone), SoftwareApplication, LocalBusiness |
| Logic | No schema present, or WebAPI/APIReference |

## Detection Algorithm

1. **Check GEO Spec Page Map** — if a match exists, classification is done.
2. **Score signals:** path match = 3 points, each code pattern = 2 points, schema hint = 2 points.
3. **Interpret the score:**
   - Score >= 5: confident classification
   - Score 2-4: likely classification, confirm with user
   - Score < 2: uncertain, ask the user

## User Confirmation Prompt

### Single File

```
이 페이지는 [상설페이지 — 제품 소개]로 보입니다.

근거:
- 파일 경로: /pricing/ 디렉토리
- 코드 패턴: PricingTable 컴포넌트, 가격 데이터 배열
- 스키마: Product 스키마 존재

맞나요? (Content / Standing / Logic 중 다른 유형이면 알려주세요)
```

### Multi-File (Directory/Project Audit)

```
총 12개 페이지 분석:
- Content: 7개 (/blog/*, /guides/*)
- Standing: 4개 (/pricing, /about, /product, /features)
- Logic: 1개 (/api/*)

확인해주세요. 변경이 필요한 페이지가 있으면 알려주세요.
```

## Mixed-Purpose Pages

Pages that span types get classified by **primary intent**. A product page with an embedded blog-style guide section is Standing (primary) with Content elements. Apply the Standing checklist first, but also follow Content principles (clear headings, quotable prose) for the Content sections within the page.

When in doubt, ask: "If an AI mentions this page, would it *quote* it (Content) or *recommend* it (Standing)?"

## Updating the Page Map

After the user confirms classification, if `geo-spec/` exists, offer to append the confirmed mapping to `geo-spec/page-map.md`. This ensures future runs skip heuristics for that path and use the declared purpose directly.
