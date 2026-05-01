# web-search Skill

**Your powerful and reliable web research assistant.**

This skill transforms how you gather information from the internet. It combines the best tools to deliver:

- **Human-like browsing** that avoids bot blocks
- **Parallel research** from multiple sources at once
- **Automatic saving** of every finding with proper citations
- **Deep, well-structured synthesis** with beautiful citations
- **Trustworthy outputs** based on real persisted data, not just memory

Research becomes effortless, thorough, and professional.

## How to Use It

Simply ask any research question in natural language:

- "Research the current state of AI coding agents in 2026"
- "Compare the top options for autonomous agents"
- "What are the latest developments in LangChain?"
- "Find recent papers about multi-agent systems"

The skill will automatically activate, run parallel searches, scrape relevant pages in a human-like way, save everything durably, and return a well-cited, high-quality summary.

The skill will instruct the agent to:

1. Create a dated research folder
2. Launch parallel workers
3. Persist every source immediately
4. Synthesize from disk with citations

## Installation

Copy the skill folder into your agent's skills directory:

```bash
rm -rf ~/.agents/skills/web-search
cp -r skills/web-search ~/.agents/skills/web-search
```

```powershell
Remove-Item -Recurse -Force ~/.agents/skills/web-search -ErrorAction SilentlyContinue
Copy-Item -Recurse skills\web-search ~/.agents/skills/web-search
```

Restart the agent or reload skills for the new skill discovery.

## Recommended Supporting Skills

This skill works even better when these referenced skills are also installed:

- [agent-browser](https://github.com/vercel-labs/agent-browser) — web scraping via browser
- [human-search](https://github.com/arterm-sedov/human-search-skill) — cascaded search
- [deep-research](https://github.com/arterm-sedov/deep-research) — synthesis and reporting
- [searxng-agent-skills](https://github.com/arterm-sedov/searxng-agent-skills) — search using SearXNG instead of Tavily
- [browser-switch](https://github.com/arterm-sedov/browser-switch) — browser agent selection
- [playwright-cli](https://github.com/microsoft/playwright-cli) — browser automation and scraping via the Playwright CLI
