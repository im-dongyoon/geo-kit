---
name: geo-kit:spec
description: >
  Create, read, and update the project's GEO Spec — a modular configuration
  that stores brand identity, page purpose mappings, target prompts, schema
  defaults, and infrastructure status. Use this skill when users want to
  initialize GEO for a project, check their GEO configuration, update page
  mappings, or manage their GEO spec. Also activate when audit/build detects
  no existing spec.
user-invocable: true
argument-hint: "[create | update <module> | (no args = read)]"
effort: medium
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
---

# GEO Spec — Project GEO Configuration Manager

Manage a project's GEO Spec: a modular directory (`geo-spec/`) at the project root that stores GEO context. Once created, the `audit` and `build` skills reference it for instant page purpose detection, schema generation, and brand-aware checks.

For the full spec format and module definitions, read `../../references/geo-spec.md`.

---

## Spec Directory Structure

```
geo-spec/
├── identity.md          — Brand, domain, industry, target customers, competitors
├── page-map.md          — Path → purpose (Content/Standing/Logic) mappings
├── target-prompts.md    — AI search queries the project wants to appear in
├── schema-defaults.md   — Organization @id, language, currency defaults
└── infra-status.md      — robots.txt, llms.txt, sitemap status + last audit date
```

---

## Workflow

### Detect Mode

| Invocation | Mode |
|------------|------|
| `/geo-kit:spec` | **Read** — show current spec summary |
| `/geo-kit:spec create` | **Create** — generate spec from project analysis |
| `/geo-kit:spec update page-map` | **Update** — modify a specific module |
| `/geo-kit:spec update identity` | **Update** — modify a specific module |

If no `geo-spec/` directory exists and mode is Read, switch to Create automatically.

---

### Create Mode

Generate the GEO Spec by analyzing the project. Follow these steps:

**Step 1: Scan Project**

Gather information from:
- `package.json` — project name, description, homepage URL
- Existing JSON-LD / schema markup — Organization info, @type patterns
- Page/route structure — detect all routes and their likely purposes
- `robots.txt` — current crawler configuration
- `sitemap.xml` — existing sitemap
- `.env` / config files — domain, API URLs (read names only, not secrets)
- README or docs — project description

**Step 2: Draft Each Module**

Generate drafts for all 5 modules based on scan results. For fields that can't be auto-detected, insert `[TODO: ...]` placeholders.

Present the drafts to the user module by module:

```
## identity.md (초안)
- 이름: [detected or TODO]
- 도메인: [detected from package.json homepage]
- 산업: [TODO: 어떤 산업/분야인가요?]
- 타겟 고객: [TODO: 주요 고객은 누구인가요?]
- 경쟁사: [TODO: 주요 경쟁사는?]

이 정보가 맞나요? 수정하거나 빈 항목을 채워주세요.
```

**Step 3: User Confirmation**

- Present each module's draft for review
- Fill in TODO items from user responses
- Make corrections as requested

**Step 4: Save**

Write all 5 files to `geo-spec/` at the project root. Each file uses YAML frontmatter:

```yaml
---
type: identity
last-updated: 2026-04-06
version: 1
---
```

Report: "GEO Spec 생성 완료. `geo-spec/` 디렉토리에 5개 모듈이 저장되었습니다."

---

### Read Mode

Summarize the current spec state. Output format:

```
## GEO Spec 현황

### Identity
- 브랜드: [name] ([domain])
- 산업: [industry]
- 타겟: [target customers]

### Page Map
- 등록된 페이지: [N]개
  - Content: [n]개
  - Standing: [n]개
  - Logic: [n]개

### Target Prompts
- Primary: [n]개
- Secondary: [n]개

### Schema Defaults
- Organization @id: [value]
- 언어: [lang] / 통화: [currency]

### Infra Status
- 마지막 audit: [date]
- robots.txt: [status] | llms.txt: [status] | sitemap: [status]
- 전체 점수: [score]/100
```

---

### Update Mode

Update a specific module. Accepted module names:
- `identity` — brand, domain, industry info
- `page-map` — add/remove/change page purpose mappings
- `target-prompts` — add/remove target AI queries
- `schema-defaults` — change Organization @id, language, currency
- `infra-status` — usually auto-updated by audit, but can be manual

**Update workflow:**
1. Read the current module file
2. Show current values to the user
3. Ask what to change
4. Apply changes and update `last-updated` in frontmatter
5. Increment `version` in frontmatter

---

## Page Purpose Types

For reference when populating `page-map.md`:

| Purpose | Goal | AI Behavior | Example Paths |
|---------|------|-------------|---------------|
| **Content** | Citation | AI quotes this page as source | /blog/*, /guides/*, /docs/* |
| **Standing** | Recommendation | AI recommends this product/service | /pricing, /about, /product/*, /features |
| **Logic** | Crawlability | AI can access the data | /api/*, middleware, SSR routes |

For detailed detection signals, read `../../references/page-purpose-detection.md`.

---

## Integration with Other Skills

- **audit** checks for `geo-spec/` at Step -1. If missing, suggests running `/geo-kit:spec create`. If present, loads Page Map for instant purpose detection and uses identity for brand checks.
- **build** checks for `geo-spec/` at Step -1. Uses Schema Defaults for JSON-LD generation and identity for brand name insertion.
- After audit completes, it offers to update `infra-status.md` with the latest results.

---

## Principles

1. **Progressive enrichment** — Start with what can be auto-detected, fill gaps over time
2. **User confirms everything** — Never save spec data without user review
3. **Lightweight** — No heavy process, just create/read/update
4. **Version tracked** — Each module has a version number in frontmatter
5. **Commit-friendly** — `geo-spec/` should be committed to version control
