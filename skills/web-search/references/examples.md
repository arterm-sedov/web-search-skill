# Examples

## Basic Research Flow

When the user asks: "Research the current state of AI coding agents in 2026"

1. Create dated folder `docs/research/20260430_ai_coding_agents/`
2. Launch parallel workers:
   - Discovery worker using searxng-search
   - Scraping worker using agent-browser (human-like navigation + snapshots)
   - Synthesis worker using deep-research patterns
3. After each result → immediately append checkpoint to `findings.md`
4. After gathering enough sources → generate `90_synthesis.md` with proper citations
5. Final answer references the persisted artifacts

The skill makes this process automatic and reliable.

See the main SKILL.md for the full checklist.
