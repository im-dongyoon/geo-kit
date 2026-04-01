# Changelog

## 2.0.0 (2026-04-01)

### Breaking Changes

- Restructured to official plugin pattern (`skills/` directory)
- Removed `init` skill — replaced by `build` skill with auto-detect
- Skill names changed: `geo-kit:build`, `geo-kit:audit`

### New

- `geo-kit:build` — Create GEO-optimized web pages with auto-detection for page creation requests
- `geo-kit:audit` — Audit existing pages with 100-point scoring and 31-point checklist
- Each SKILL.md is self-contained with key GEO content inlined
- Pushy descriptions for better auto-triggering

### Fixed

- Skill discovery failure (root SKILL.md missing)
- Reference file path resolution (references unreachable from subdirectories)
- Skill name namespace duplication (`geo-kit:geo-kit:*`)

## 1.0.0 (2026-03-24)

### Initial Release

- SKILL.md with GEO audit & build workflows
- 6 reference guides:
  - Core principles & content structure design
  - Page type templates with checklists and before/after examples
  - Schema markup (JSON-LD) implementation guide
  - AI crawler access management
  - Platform-specific optimization strategies & KPIs
  - 31-Point Citation Readiness Checklist
