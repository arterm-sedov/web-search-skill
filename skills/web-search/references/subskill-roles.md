# Sub-Skill Roles in web-search Orchestration

## Role Mapping

- **human-search**: Primary intelligent cascade. Handles tiered fallback (native → Python scraper → browser CLI). Use as default retrieval engine for robustness.
- **agent-browser**: Primary anti-bot scraping tool. Follow core workflow: `open` → `snapshot -i` → extract using refs → `re-snapshot` after changes. Use named sessions for parallel work.
- **searxng-search / searxng-extract**: Fast, free, unlimited local discovery and content extraction layer. Ideal for initial URL candidate gathering without API keys.
- **deep-research**: Final synthesis phase. Provides structured reporting, citation management, progressive disclosure, and professional formatting for the `90_synthesis.md` file.
- **browser-switch**: Decides between agent-browser, playwright-cli, or other browser backends based on context.
- **playwright-cli**: Backup browser automation when agent-browser is unavailable or for specific Playwright features.

This mapping ensures `web-search` is comprehensive without code duplication — it orchestrates rather than reimplements.
