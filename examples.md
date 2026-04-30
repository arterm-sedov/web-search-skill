# web-search Skill - Examples

## Example 1: Parallel Research Task

```markdown
User: Research the current state of LangChain agent patterns in 2026.

Workflow:
1. Create docs/research/20260430_langchain_agents/
2. Launch 3 parallel Task subagents:
   - Subagent 1: searxng-search for recent papers and repos
   - Subagent 2: agent-browser to scrape key documentation pages with snapshots
   - Subagent 3: deep-research patterns for synthesis
3. After each result:
   - Immediately append checkpoint to findings.md
   - Example checkpoint:
     ### 2026-04-30 12:05:22 - Source 1
     **Source**: https://python.langchain.com/docs
     **Method**: browser-rendered
     **Raw Evidence**: > LangChain 0.3 introduces new LCEL patterns...
     **Insight**: Core patterns have stabilized around runnables and tool calling.
     **Confidence**: high
4. After gathering 8+ sources, synthesize into 90_synthesis.md with citations.
```

## Example 2: Anti-Bot Scraping

When a site blocks simple requests:
- Use `agent-browser open https://target.com && agent-browser snapshot -i`
- Extract using refs from snapshot
- Immediately persist the rendered content as checkpoint
- Reference human-search Tier 3 (browser CLI) as fallback

## Example 3: Using Referenced Skills

```bash
# In parallel subagents:
# 1. Use human-search for cascade
# 2. Use agent-browser for JS-heavy pages
# 3. Use deep-research for final report formatting with citations
```

See `reference.md` for full checkpoint template and sub-skill mapping.
