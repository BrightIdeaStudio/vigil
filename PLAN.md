# Vigil — Platform Health Monitor & Auto-Fix

> **Roadmap & tasks**: See [GitHub Issues](https://github.com/BrightIdeaStudio/vigil/issues) and the [BIS Project Board](https://github.com/orgs/BrightIdeaStudio/projects/1).

## Context

Vigil is the platform health monitor and auto-fix system for the BrightIdeaStudio suite. It's developer-facing (for Kyle as platform creator), not user-facing (that's Lumen).

```
Synapse (ideas) → Atelier (agents) → Beacon (execution) ← Lumen (observation)
                                                          ← Vigil (platform health)
```

Vigil sits alongside Lumen but serves a different audience:
- **Lumen**: "How is my AI session going?" (end user)
- **Vigil**: "Is the platform healthy? What bugs need fixing?" (platform developer)

**Repo:** `BrightIdeaStudio/vigil`
**Directory:** `~/dev/BrightIdeaStudio/vigil`

## Authority Boundaries

| Vigil (this project)                  | NOT Vigil                             |
|---------------------------------------|---------------------------------------|
| Collect error logs & crash reports    | Monitor user sessions (Lumen)         |
| Analyze failures & root causes        | Route LLM calls (Beacon)             |
| Propose fixes with test plans         | Compose agent teams generically (Atelier) |
| Execute fixes with approval           | Incubate ideas (Synapse)             |
| Track fix lifecycle                   | Enforce user budgets (Lumen)          |
| Performance regression detection      | Score models by cost/quality (Beacon) |

## What Vigil Monitors

- Error logs from all suite projects
- Crash reports and unhandled exceptions
- Performance metrics (response times, throughput)
- CI/CD pipeline failures
- User bug reports and bad experience signals

## Data Sources

- Project log files (`data/` directories)
- CI output (GitHub Actions)
- Error tracking (structured error events from each project's API)
- User feedback (GitHub issues, support tickets)

## Fix Lifecycle

```
Detected → Analyzed → Proposed → Approved → Fixed → Verified
```

1. **Detected** — error pattern identified from logs/reports
2. **Analyzed** — root cause determined, affected components identified
3. **Proposed** — fix plan generated with test strategy
4. **Approved** — human reviews and approves (or auto-approved if low-risk)
5. **Fixed** — changes applied, branch created, tests run
6. **Verified** — fix confirmed working, PR merged

## Autonomy Configuration

Configurable per risk level:

### Human-in-the-Loop (default)
Vigil detects and proposes fixes, but requires explicit approval before executing any changes.

### Auto-Fix Policies (configurable)
Users define what Vigil can fix automatically:
- **Low risk (auto-fix eligible)**: test failures, lint issues, dependency updates, typo fixes
- **Medium risk (approval required)**: API changes, schema changes, configuration changes
- **High risk (always manual)**: architecture changes, data migrations, security fixes, breaking changes

## Integration with Other Projects

- **Receives data from all projects** — each project's FastAPI server exposes a health/error endpoint
- **Uses Atelier** for composing agent teams when fixes require multi-step orchestration
- **Routes through Beacon** for AI analysis tasks (error pattern recognition, root cause analysis)
- **Reports to Lumen** — fix activity appears as events in the platform activity stream

## Architecture (placeholder)

Will follow suite conventions when implementation begins:
- Package: `src/vigil/`
- Interfaces: MCP server + Typer CLI + FastAPI + React web dashboard
- Data models: Pydantic
- Storage: JSON files, abstractable to Supabase
- Default port: 8400

Full implementation plan deferred until after Lumen and Atelier are built. Vigil depends on the inter-project communication layer (built in Lumen v0.1) and agent composition (built in Atelier v0.1).
