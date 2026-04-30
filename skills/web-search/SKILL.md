---
name: web-search
description: Your powerful, reliable web research companion. This skill delivers high-quality multi-source research with excellent anti-bot resilience, intelligent browser scraping, parallel discovery, deep synthesis, and beautifully cited outputs. Always reach for this skill whenever you need to search the web, research any topic, scrape information, find the latest data, or compare options. It makes research effortless, thorough, and trustworthy.
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

All referenced skills are available on GitHub. Install any missing ones by copying the skill folder into your agent's skills directory.

- **[human-search](https://github.com/arterm-sedov/human-search-skill)**: Intelligent cascade engine (native → Python scraper → browser CLI → crawl4ai). Core retrieval fallback chain.
- **[agent-browser](https://github.com/vercel-labs/agent-browser)**: Primary human-like browser scraping tool. Follow `open → snapshot -i → extract → re-snapshot` pattern. Strongest anti-bot resilience.
- **[searxng-search](https://github.com/arterm-sedov/searxng-agent-skills)** + **[searxng-extract](https://github.com/arterm-sedov/searxng-agent-skills)**: Free, unlimited local search and extraction (no API keys). Excellent for discovery phase.
- **[deep-research](https://github.com/arterm-sedov/deep-research)**: High-quality synthesis, citations, structured reporting, and progressive disclosure. Use for final synthesis.
- **[browser-switch](https://github.com/arterm-sedov/browser-switch)**: Selects optimal browser automation backend.
- **[playwright-cli](https://github.com/microsoft/playwright-cli)**: Strong alternative browser automation tool.

**Tip**: After installing missing skills, restart your agent session so they are discovered. Update the GitHub username/organization in the links above when you publish the repositories.

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
See `references/examples.md` for concrete parallel Task usage and `references/reference.md` for full checkpoint template.

## Integration with AGENTS.md
This skill is the canonical implementation of the **Web Research Policy** section in AGENTS.md. All agents should route web research through this skill to ensure consistency, persistence, and quality.

---
**Remember**: Research is not complete until artifacts are durably written to disk and synthesis is based on them.
