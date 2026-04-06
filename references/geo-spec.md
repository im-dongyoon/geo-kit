# GEO Spec -- Project-Level GEO Configuration

> When to read this: When creating, reading, or updating a project's GEO spec. Referenced by the `spec`, `audit`, and `build` skills.

---

## What is a GEO Spec?

A GEO spec is a modular directory (`geo-spec/`) placed at a project's root that stores all GEO context for that project -- brand identity, page purposes, target AI prompts, schema defaults, and infrastructure status. It is created once (typically via the `spec` skill), referenced by every `audit` and `build` run, and grows richer over time as new pages are added or strategy evolves.

## Directory Structure

```
geo-spec/
  identity.md          # Brand info & domain context
  page-map.md          # Page inventory with purpose tags
  target-prompts.md    # AI search queries to rank for
  schema-defaults.md   # Shared JSON-LD values
  infra-status.md      # Infrastructure health (auto-updated)
```

---

## Module Definitions

### identity.md

```markdown
---
type: identity
last-updated: 2026-03-15
version: 1
---

# Brand

- **Name:** Roomly
- **Domain:** roomly.io
- **Logo URL:** https://roomly.io/logo.svg
- **Social:** @roomly (X), /roomly (LinkedIn)

# Domain Context

- **Industry:** Virtual office / remote collaboration
- **Target Customers:** Distributed teams (20-500 employees)
- **Competitors:** Gather, Teamflow, Kumospace
- **Core Value Proposition:** Spatial audio virtual office that reduces meeting fatigue by 40%
```

### page-map.md

```markdown
---
type: page-map
last-updated: 2026-03-15
version: 1
---

| Path Pattern | Purpose | Description | Key Prompt |
|---|---|---|---|
| `/` | Standing | Homepage -- brand intro & social proof | "best virtual office platform" |
| `/product` | Standing | Feature overview with comparison tables | "virtual office software features" |
| `/blog/spatial-audio-*` | Content | Educational posts on spatial audio | "what is spatial audio for remote work" |
| `/pricing` | Logic | Plan comparison, crawlable pricing table | "roomly pricing" |
| `/docs/**` | Logic | Developer docs, API reference | "roomly API integration" |
```

**Purpose types:**
- **Content** -- The page's goal is AI citation (appear as a quoted source in AI answers).
- **Standing** -- The page's goal is AI recommendation (be named when AI suggests solutions).
- **Logic** -- The page's goal is AI crawlability (ensure AI can read and index the content correctly).

### target-prompts.md

```markdown
---
type: target-prompts
last-updated: 2026-03-15
version: 1
---

# Primary Prompts (must appear)

These are the AI search queries the project must be cited or recommended for.

1. "best virtual office platform for remote teams"
2. "virtual office software with spatial audio"
3. "how to reduce Zoom fatigue for distributed teams"

# Secondary Prompts (nice to have)

1. "virtual office vs video conferencing"
2. "spatial audio collaboration tools"
3. "remote team engagement software"
```

### schema-defaults.md

```markdown
---
type: schema-defaults
last-updated: 2026-03-15
version: 1
---

- **Organization @id:** https://roomly.io/#organization
- **WebSite @id:** https://roomly.io/#website
- **Default Language:** en
- **Currency:** USD
```

### infra-status.md

```markdown
---
type: infra-status
last-updated: 2026-04-01
version: 3
---

- **Last Audit Date:** 2026-04-01
- **robots.txt:** PASS -- AI crawlers allowed
- **llms.txt:** PASS -- present at /llms.txt
- **sitemap.xml:** WARN -- missing lastmod dates
- **Overall Score:** 82 / 100
```

> This file is auto-updated after each `audit` run. Do not edit manually.

---

## How Skills Use the Spec

### audit

- **Page Map** -- instant purpose detection per URL, skipping heuristic analysis.
- **Identity brand name** -- used for Entity Clarity checks (does the page clearly state who it represents?).
- **Target Prompts** -- evaluated against H1/H2 content for relevance alignment.
- **infra-status** -- overwritten with fresh results after audit completes.

### build

- **Schema Defaults** -- auto-populate `@id`, language, and currency in generated JSON-LD.
- **Identity brand/domain** -- auto-insert brand name and canonical domain in generated code.
- **Page Map purpose** -- select the correct template and GEO principles (Content pages get citation-first structure, Standing pages get comparison tables).

### spec (management)

- **Create:** Analyze the project (package.json, existing schemas, page structure, domain info), generate module drafts, present for user confirmation, then save to `geo-spec/`.
- **Read:** Summarize the current spec state across all modules.
- **Update:** Modify specific modules while preserving the rest.

---

## Creation Guide

The `spec` skill auto-generates each module by analyzing available project signals:

| Module | Analysis Source |
|---|---|
| identity.md | package.json (`name`, `description`, `homepage`), existing schema markup, README |
| page-map.md | File-system routes or framework router config, existing page titles and meta descriptions |
| target-prompts.md | Page content headings, meta keywords, identity context, competitor analysis |
| schema-defaults.md | Existing JSON-LD in any page, package.json `homepage` field |
| infra-status.md | Direct checks of robots.txt, llms.txt, sitemap.xml at the live domain |

---

## Best Practices

- **Keep page-map.md current** -- add new pages as they are created, remove deprecated routes.
- **Review target-prompts.md quarterly** -- align with marketing strategy and evolving AI search trends.
- **Do not manually edit infra-status.md** -- let the `audit` skill update it with each run.
- **Commit `geo-spec/` to version control** -- it is project configuration, not a build artifact.
- **One spec per project** -- monorepos with multiple sites should have one `geo-spec/` per deployable site.
