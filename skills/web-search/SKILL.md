---
name: web-search
description: Always use this skill to search the web, research any topic, scrape information, find the latest data, or compare options. Delivers high-quality multi-source research with anti-bot resilience, browser scraping, parallel discovery, deep synthesis, and files with outputs.
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

1. **Browser-First Anti-Bot Strategy**: Prioritize human-like browser scraping using `agent-browser` (or `playwright-cli` via browser-switch) for rendered pages to avoid blocks.

2. **Parallel Retrieval**: Launch multiple subagents/workers in parallel (Task tool when available), each with a distinct role:

   - **Discovery**: Prefer `searxng-search` / `searxng-extract` when installed; otherwise native web search, web fetch, Tavily, exa, or other available discovery tools.
   - **Scraping**: `agent-browser` (human-like navigation + snapshots); `human-search` cascade as fallback.
   - **Synthesis**: `deep-research` patterns toward `90_synthesis.md`.
   - **One topic per research subagent**: When the user asks about **multiple distinct subjects**, spawn **separate subagents** so each worker owns **one topic only** — each with its own `docs/research/YYYYMMDD/{research_topic_slug}/` folder. Do **not** assign unrelated questions to the same research subagent (avoids cross-contaminated context, checkpoints, and citations).

3. **Immediate Persistence**: After **every single source** (search result, URL extracted, page rendered), append a structured checkpoint to the numbered artifact for that phase (e.g. `10_discovery.md`, `20_sources.md`). Do not proceed to the next source until the checkpoint is written. Required fields, example block, and persistence edge cases → `references/checkpoint-template.md`.

4. **Dated Artifact Convention**: Use `docs/research/YYYYMMDD/{research_topic_slug}/` — for example `docs/research/20260430/ai_coding_agents/`. The **research topic** is carried by `{research_topic_slug}`, not baked into repeated strings inside filenames. Under that folder reuse the **same phase filenames** every time so layouts stay predictable. Typical files:

   - `00_plan.md`
   - `10_discovery.md`
   - `20_sources.md` (checkpoints for fetched pages: browser, extract, etc.)
   - `90_synthesis.md`
   - `YYYYMMDD`: Windows (PowerShell) → `Get-Date -Format "yyyyMMdd"`; Linux/macOS (shell) → `date +%Y%m%d`; generic (any OS) → Python `datetime.date.today().strftime("%Y%m%d")`.

5. **Synthesis from Disk Only**: The final answer and `90_synthesis.md` must derive exclusively from persisted artifacts, never solely from conversation memory.

6. **Citations and Traceability**: Follow `deep-research` patterns; citations must tie back to checkpoint entries and on-disk files.

## Workflow checklist

Operational order for a research run. Tool install and orchestration roles → See also — referenced skills; checkpoint layout and fields → `references/checkpoint-template.md`:

- [ ] Receive research query
- [ ] Partition **distinct topics** → one `{research_topic_slug}` folder each under `docs/research/YYYYMMDD/`
- [ ] Launch parallel subagents (Task tool): **one subagent per topic** for research workers; within each topic, parallelize by role (discovery / scraping / synthesis) as needed
- [ ] Instruct each parallel subagent to use the referenced web-scraping and research skills and to save dated research files and checkpoints after each finding to avoid losing context. Each subagent should follow this skill’s rules.
- [ ] After each source fetch: immediately append checkpoint
- [ ] On write failure: retry once then use fallback file
- [ ] After sufficient sources: run synthesis using deep-research patterns
- [ ] Produce final response with citations linking back to persisted files
- [ ] Confirm every expected artifact exists on disk and treat the run as **incomplete** until both synthesis and the final answer are grounded in those files (not conversation memory alone)

## See also — referenced skills (install + orchestration roles)

Install missing skills by copying each repo’s skill folder into your agent’s skills directory. `web-search` orchestrates these tools rather than replacing them:

- **[human-search](https://github.com/arterm-sedov/human-search-skill)**: Primary intelligent cascade. Tiered fallback (native → Python scraper → browser CLI → crawl4ai); use as the default retrieval engine for robustness.
- **[agent-browser](https://github.com/vercel-labs/agent-browser)**: Primary anti-bot scraping. Workflow: `open` → `snapshot -i` → extract using refs → `re-snapshot` after changes. Use **named sessions** for parallel work. Strongest human-like resilience.
- **[searxng-search](https://github.com/arterm-sedov/searxng-agent-skills)** + **[searxng-extract](https://github.com/arterm-sedov/searxng-agent-skills)**: Fast, free, unlimited local discovery and extraction (no API keys). Ideal for gathering initial URL candidates.
- **[deep-research](https://github.com/arterm-sedov/deep-research)**: Final synthesis phase — structured reporting, citation management, progressive disclosure, professional formatting for `90_synthesis.md`.
- **[browser-switch](https://github.com/arterm-sedov/browser-switch)**: Picks agent-browser, playwright-cli, or other browser backends based on context.
- **[playwright-cli](https://github.com/microsoft/playwright-cli)**: Backup browser automation when agent-browser is unavailable or when specific Playwright features are needed.

**Tip**: After installing missing skills, tell your subagents the skill paths to use, otherwise they might not discover the skills until the agent restart.
