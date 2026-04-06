# Framework-Specific GEO Pitfalls

> When to read this: When auditing or building pages in a specific framework. These are non-obvious traps that silently break GEO — not general principles, but framework-specific gotchas.

---

## Next.js — App Router

### `loading.tsx` Blocks Content from Crawlers
**Pitfall:** `loading.tsx` wraps the page in a `<Suspense>` boundary. AI crawlers receive the loading fallback UI instead of actual content.
**Fix:** Remove `loading.tsx` from public-facing route segments, or move critical content above the Suspense boundary in `layout.tsx`. Keep `loading.tsx` only for authenticated/internal pages.

### Client Components Cannot Export Metadata
**Pitfall:** Adding `'use client'` to a page component prevents `export const metadata` or `generateMetadata()` from working. Meta tags silently disappear.
**Fix:** Keep metadata exports in Server Components. If the page needs client interactivity, split into a Server Component wrapper (with metadata) and a Client Component child.

### `generateStaticParams` Required for Dynamic Routes
**Pitfall:** Dynamic routes (`/blog/[slug]`) without `generateStaticParams` are not pre-rendered at build time. Crawlers must trigger on-demand rendering, which may time out or return incomplete HTML.
**Fix:** Implement `generateStaticParams` for all public dynamic routes. This pre-renders pages at build time, ensuring crawlers always get complete HTML.

### `_next/static/` Wastes Crawl Budget
**Pitfall:** Next.js serves CSS, JS, and other assets under `/_next/static/`. If not blocked in robots.txt, AI crawlers spend budget crawling these non-content files.
**Fix:** Add `Disallow: /_next/static/` to robots.txt default rules.

### Route Groups Affect Crawl Paths
**Pitfall:** Route groups `(marketing)`, `(app)` don't appear in URLs but can cause confusion if layouts are structured incorrectly — different groups may serve duplicate content at the same URL.
**Fix:** Ensure each public URL resolves to exactly one page component. Use route groups only for layout organization, not content separation.

---

## Next.js — Pages Router

### `getServerSideProps` vs `getStaticProps` Impact
**Pitfall:** `getServerSideProps` runs on every request, increasing response time for crawlers. If the data source is slow, crawlers may time out.
**Fix:** Use `getStaticProps` with `revalidate` (ISR) for public pages. Reserve `getServerSideProps` for pages requiring real-time data per request.

---

## SPA Frameworks (React, Vue, Angular — CSR)

### Empty Initial HTML
**Pitfall:** Pure CSR apps serve a minimal HTML shell (`<div id="root"></div>`). AI crawlers see an empty page with no content to extract or cite.
**Fix:** Add SSR/SSG capability (Next.js, Nuxt, Remix, Astro) or use a pre-rendering service. Verify with `curl -s URL | head -50` — if no content visible, crawlers can't see it either.

### Client-Side Routing is Invisible
**Pitfall:** SPA routers (React Router, Vue Router) handle navigation client-side. Crawlers see only the initial page — they don't click links or trigger route changes.
**Fix:** Ensure all important pages are accessible as direct URLs with server-rendered content. Don't rely on client-side navigation for content discovery.

### Dynamic Imports / Lazy Loading
**Pitfall:** `React.lazy()`, dynamic `import()`, and route-level code splitting may defer critical content behind JavaScript execution. Crawlers that don't execute JS fully miss this content.
**Fix:** Ensure GEO-critical content (H1, opening paragraph, FAQ, schema) is in the initial render, not behind lazy-loaded components. Lazy-load only non-essential UI (modals, below-fold widgets).

---

## Astro

### Islands Architecture Content Gap
**Pitfall:** Astro's islands architecture renders interactive components client-side. If GEO-critical content is inside an island component, it may not appear in the static HTML.
**Fix:** Keep all GEO signals (H1, opening text, FAQ, schema) in static Astro components, not inside `client:*` islands. Islands should be for interactivity only (forms, counters, dynamic UI).

---

## SvelteKit

### `+page.ts` vs `+page.server.ts`
**Pitfall:** `+page.ts` load functions run on both client and server, but `+page.server.ts` runs only on the server. If sensitive data fetching is in `+page.ts`, it may expose API keys client-side. If content fetching is only client-side, crawlers miss it.
**Fix:** Use `+page.server.ts` for data fetching that should produce content visible to crawlers. The data returned will be serialized into the initial HTML.

---

## CMS Platforms (Sanity, Contentful, Strapi, etc.)

### Content Model Missing GEO Fields
**Pitfall:** CMS content models often have a single "body" rich text field. GEO requires separate, structured fields: TL;DR, FAQ pairs, author info, meta description. When these are embedded in the body, automated schema generation is impossible.
**Fix:** Add dedicated fields to the content model:
- `tldr` (text) — Key takeaways, separate from body
- `faq` (array of {question, answer}) — Structured FAQ pairs
- `author` (reference) — Author with credentials and external links
- `metaDescription` (text) — Separate from body content
- `publishedAt` / `updatedAt` (datetime)

### Preview/Draft Content Leaking to Crawlers
**Pitfall:** CMS preview modes may serve draft content to crawlers if preview URLs are not properly gated.
**Fix:** Ensure preview routes have `noindex` and are behind authentication. Only published content should be accessible to crawlers.

---

## Universal Detection

When auditing, detect the framework by checking:

| Signal | Framework |
|--------|-----------|
| `next.config.*` | Next.js |
| `nuxt.config.*` | Nuxt |
| `astro.config.*` | Astro |
| `svelte.config.*` | SvelteKit |
| `vite.config.*` + no framework config | Vite SPA |
| `angular.json` | Angular |
| CMS SDK imports (`@sanity/client`, `contentful`) | Headless CMS |

Then check for the framework-specific pitfalls listed above.
