# web-search Skill - Reference

## Checkpoint Template

Use this exact structure for every source. Append to the appropriate dated findings file.

```markdown
### 2026-04-30 12:05:22 - Source 3

**Source**: https://example.com/article
**Method**: browser-rendered (agent-browser)
**Raw Evidence**:
> "Exact quote or key paragraph from the page."

**Insight**: 1-2 sentence key takeaway or conclusion.

**Confidence**: high

---
```

## Persistence Rules
- Path pattern: `docs/research/YYYYMMDD/{topic_slug}/findings.md`
- Generate date using native commands (see AGENTS.md)
- Write **immediately** after each source
- On failure: retry once, then use `findings_fallback.md`

## Sub-Skill Roles
- **human-search**: Core intelligent cascade
- **agent-browser**: Primary rendered scraping engine (recommended first choice)
- **searxng-search/extract**: Fast local discovery
- **deep-research**: Final high-quality synthesis and citation formatting
- **browser-switch**: Chooses best browser tool
- **playwright-cli**: Alternative browser backend

This skill is designed to make research reliable, persistent, and high-quality while staying enjoyable to use.
