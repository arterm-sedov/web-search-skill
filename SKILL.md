---
name: web-search
description: ALWAYS use this skill for ANY web search, research, scraping, extraction, comparison, latest information, or "find sources on the web" task. Never perform web research without invoking this skill first. Delivers reliable, multi-channel research with strong anti-bot resilience through human-like browser scraping, parallel retrieval workers, immediate persistence of every source to dated files, deep-research-grade synthesis with proper citations, and final answers derived exclusively from on-disk artifacts. Orchestrates and builds upon: human-search (cascade engine), agent-browser (primary rendered scraping and sessions), searxng-search/searxng-extract (discovery), deep-research (structured synthesis and reporting), browser-switch, and playwright-cli.
---

# web-search Skill

## When to Use
**ALWAYS** invoke this skill for any task involving:
- Web search
- Research or deep investigation
- Scraping or data extraction from websites
- Finding latest/current information
- Comparing options from web sources
- Any "find on the web" or "research X" request

Never perform web research using only transient memory or single-channel tools.

## Core Principles (MUST Follow)
1. **Browser-First Anti-Bot Strategy**: Prioritize human-like browser scraping using `agent-browser` (or playwright-cli via browser-switch) for rendered pages to avoid blocks.
2. **Parallel Retrieval**: Launch multiple subagents/workers in parallel (use Task tool when available) with distinct strategies:
   - One for discovery (searxng-search)
   - One for deep scraping (agent-browser + human-search)
   - One for synthesis (deep-research patterns)
3. **Immediate Persistence**: After **every single source** (search result, URL extracted, page rendered), immediately write a structured checkpoint to a dated file. Do not proceed to the next source until the checkpoint is written.
4. **Dated Artifact Convention**: Use `docs/research/YYYYMMDD/{topic_slug}/` with files like:
   - `00_plan.md`
   - `10_discovery.md`
   - `20_browser_findings.md`
   - `90_synthesis.md`
   - Use native date commands from AGENTS.md (`Get-Date -Format "yyyyMMdd"`, `date +%Y%m%d`, or Python `datetime`).
5. **Synthesis from Disk Only**: Final response must be based exclusively on persisted artifacts, never solely from conversation memory.
6. **Citations and Traceability**: Follow deep-research patterns for proper citations and source traceability.

## Checkpoint Format (Every Source)
Each checkpoint entry must include:
- Timestamp (ISO-8601)
- Source URL or identifier
- Retrieval method (browser-rendered | searxng | extract | query-search)
- Raw evidence snippet or quote
- Provisional insight (1-2 lines)
- Confidence (low|medium|high)

## See Also (Referenced Skills)
- **[human-search](../human-search/SKILL.md)**: Intelligent cascade (native websearch → Python scraper → browser CLI → crawl4ai). Use as the core retrieval engine.
- **[agent-browser](../agent-browser/SKILL.md)**: Primary tool for human-like rendered page extraction, snapshots, sessions, and anti-bot scraping. Core workflow: open → snapshot(-i) → interact/extract → re-snapshot.
- **[searxng-search](../searxng-search/SKILL.md)** and **[searxng-extract](../searxng-extract/SKILL.md)**: Free, unlimited local discovery and content extraction. Use for initial URL finding.
- **[deep-research](../deep-research/SKILL.md)**: Structured synthesis, citation management, and professional report formatting. Use for final synthesis phase.
- **[browser-switch](../browser-switch/skills/browser-switch/SKILL.md)**: Helps select optimal browser automation approach.
- **[playwright-cli](../playwright-cli/SKILL.md)**: Alternative/backup browser automation when needed.

## Workflow Checklist
- [ ] Receive research query
- [ ] Create `docs/research/YYYYMMDD/{topic}/` directory
- [ ] Launch parallel subagents (Task tool) with clear role assignment
- [ ] After each source fetch: immediately append checkpoint
- [ ] On write failure: retry once then use fallback file
- [ ] After sufficient sources: run synthesis using deep-research patterns
- [ ] Produce final response with citations linking back to persisted files
- [ ] Verify all artifacts exist on disk before concluding

## Examples
See `examples.md` for concrete parallel Task usage and `reference.md` for full checkpoint template.

## Integration with AGENTS.md
This skill is the canonical implementation of the **Web Research Policy** section in AGENTS.md. All agents should route web research through this skill to ensure consistency, persistence, and quality.

---
**Remember**: Research is not complete until artifacts are durably written to disk and synthesis is based on them.
