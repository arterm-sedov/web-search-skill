# Checkpoint template

`SKILL.md`: *when* to append (after every source, which numbered artifact). **This file**: *what* to write — layout, persistence, usage. Keep checkpoint detail here so `SKILL.md` does not repeat it.

## Persistence Rules

- Path pattern: `docs/research/YYYYMMDD/{research_topic_slug}/` — topic lives in `{research_topic_slug}`; phase files are fixed names (e.g. `10_discovery.md`, `20_sources.md`; see `SKILL.md`).
- Write **immediately** after each source fetch; do not continue until the checkpoint is appended.
- On failure: retry once, then append to `findings_fallback.md` in the same folder (or equivalent fallback named in session notes).

## Standard Entry Format

Append the fenced block once per fetched source into the matching phase file (page checkpoints → `20_sources.md` in that topic’s folder). Close each entry with `---` on its own line before the next.

Required labels (same order as the example):

- **Time**: When the checkpoint was appended, with timezone.
- **Source**: Canonical URL or stable identifier for the page/result.
- **Method**: One of `browser-rendered`, `searxng`, `extract`, `query-search`; add a parenthetical naming the concrete skill or tool path (see example).
- **Confidence**: `low/high`.
- **Insight**: One–two sentences; provisional takeaway.
- **Relevant extracted content**: Under `# …`, store what you pulled from **Source** so **Insight** stays auditable. Use `>` for quotable prose, and code fences, tables, lists.

```markdown
**Time**: 2026-04-23, 16:41:05 UTC
**Source**: https://openai.com/index/gpt-5-5-system-card/
**Method**: browser-rendered (via agent-browser snapshot)
**Confidence**: high
**Insight**: April 2026 system card summarizes GPT-5.5 as a heavier tool-using, longer-horizon model and pairs launch claims with Preparedness/red-team results (incl. cyber and bio lanes) plus “strongest safeguards to date.”

# Relevant extracted content

> "GPT-5.5 is a new model designed for complex, real-world work, including writing code, researching online, analyzing information, creating documents and spreadsheets, and moving across tools to get things done."

---
```

## Usage Rules

- Never skip saving/appending dated research files for persistence after a fetch.
- In **Method**, name how the payload was retrieved and which stack was used (`searxng`, `extract`, `browser-rendered`, etc.).
