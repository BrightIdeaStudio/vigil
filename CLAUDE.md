# Vigil — Project Conventions

## What This Project Is
Vigil is a platform health monitor and auto-fix system. It collects errors, analyzes failures, proposes fixes, and can execute them with approval. It is developer-facing (for the platform creator), not user-facing. It is part of the BrightIdeaStudio suite. See `PLAN.md` for the vision document. For roadmap and tasks, see [GitHub Issues](https://github.com/BrightIdeaStudio/vigil/issues) and the [BIS Project Board](https://github.com/orgs/BrightIdeaStudio/projects/1).

## Scope Boundaries
- Vigil handles **platform health monitoring, error analysis, and automated fixes** only
- It does NOT monitor individual user sessions (that's Lumen)
- It does NOT route tasks to LLM providers (that's Beacon)
- It does NOT compose agent teams generically (that's Atelier)
- It does NOT incubate ideas (that's Synapse)
- See `~/dev/BrightIdeaStudio/helm/SUITE_CONTEXT.md` for suite-wide context

## Tech Stack
- Python 3.12+, managed with `uv`
- Pydantic for all data models
- Typer for CLI
- FastAPI + Uvicorn for web API
- React + Vite + TypeScript for web frontend (in `web/`)
- FastMCP for MCP server
- httpx for inter-project HTTP communication

## Conventions
- Package lives in `src/vigil/`
- Entry points:
  - `python -m vigil` — MCP server (stdio)
  - `vigil` — CLI
  - `vigil serve` — FastAPI + web dashboard
- Config files in `config/`
- Runtime data in `data/`
- Default port: 8400

## Session Behavior
- **TDD**: Write tests before implementation. Create/update test files first, verify they fail, then write code to make them pass.
- **Security**: Run `bandit -r src/` after each implementation phase. Fix all HIGH and MEDIUM findings before committing.
- **Review cycle**: After implementation, run tests + bandit. If issues found, fix and re-check. Maximum 3 review-fix cycles — if an issue persists after 2 fix attempts, stop and report it to the user.
- **Phase order**: tests → implementation → test suite → bandit → review (up to 3 rounds) → commit
- Do not push to remote — the user will push when ready
