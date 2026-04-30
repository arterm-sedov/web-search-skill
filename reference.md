# web-search Skill - Reference

## Checkpoint Template

Use this exact structure for every source. Append to the appropriate dated findings file.

```markdown
### YYYY-MM-DD HH:MM:SS - Source N

**Source**: https://example.com/article
**Method**: browser-rendered (agent-browser) | searxng | extract
**Raw Evidence**:
> Exact quote or key paragraph from the page (1-3 sentences).

**Insight**: 1-2 sentence provisional conclusion or key takeaway.

**Confidence**: high | medium | low

**Tags**: #topic #subtopic
---

```

## Persistence Rules
- **Path**: `docs/research/YYYYMMDD/{topic_slug}/findings.md`
- Generate date using:
  - PowerShell: `Get-Date -Format "yyyyMMdd"`
  - Bash: `date +%Y%m%d`
  - Python: `python -c "from datetime import datetime; print(datetime.now().strftime('%Y%m%d'))"`
- Write **immediately** after each fetch. Do not batch.
- If write fails: retry once, then write to `findings_fallback.md` and log error.

## Sub-Skill Roles
- **human-search**: Primary cascade orchestrator (Tier 1-5 fallback). Use for robust retrieval.
- **agent-browser**: Main scraping engine. Follow open → snapshot(-i) → extract → re-snapshot pattern. Use named sessions for parallel work.
- **searxng-search/searxng-extract**: Fast, free, unlimited discovery layer. Use first for URL candidates.
- **deep-research**: Final synthesis, citation management, structured reporting. Use for 90_synthesis.md.
- **browser-switch**: Selects optimal browser backend when needed.

## Dated Folder Convention
```
docs/research/
  20260430_topic_slug/
    00_plan.md
    10_discovery.md
    20_browser_findings.md
    90_synthesis.md
    findings.md (append-only checkpoint log)
```

This structure ensures traceability, persistence, and compliance with AGENTS.md.
