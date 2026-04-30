# web-search Skill

Global skill for enforced, high-quality web research across all agents (Cursor, Codex, OpenCode).

## Purpose
This skill ensures all web research follows strict best practices:
- Browser-first human-like scraping (anti-bot)
- Parallel multi-channel retrieval
- Immediate persistence after every source
- Synthesis from disk artifacts only
- Proper citations via deep-research patterns

## Installation
```bash
# Global install (recommended)
cp -r "D:\Repo\web-search" "$HOME/.agents/skills/web-search"

# Or for Cursor specifically
cp -r "D:\Repo\web-search" "$HOME/.cursor/skills/web-search"
```

After installation, the skill will be automatically discovered by agents when they see research-related queries.

## Usage
Simply ask any research question. The skill will trigger automatically due to its strong description.

Example:
> Research the latest developments in LangChain agents in 2026.

The skill will:
1. Create dated research folder
2. Launch parallel workers
3. Persist every source immediately
4. Synthesize from disk with citations

## Referenced Skills
- `human-search` - cascade engine
- `agent-browser` - primary scraping
- `searxng-search` / `searxng-extract` - discovery
- `deep-research` - synthesis and reporting
- `browser-switch` - browser selection

See `SKILL.md` for full agent instructions and `reference.md` for templates.

## Publishing
This repository is designed to be published to GitHub. Agents can then reference it via marketplace tools if available.

## Compliance
Fully aligned with the **Web Research Policy** section in `AGENTS.md` (cmw-platform-agent repository).
