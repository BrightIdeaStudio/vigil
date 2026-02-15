# Vigil — Roadmap

## Current Iteration (v0.1)

Vision and planning phase. Full implementation plan deferred until Lumen and Atelier are built. See [PLAN.md](PLAN.md) for the vision document.

## Future Ideas

### Features
- `[high]` CI/CD integration (GitHub Actions, detect failures automatically)
- `[high]` Error pattern recognition (group similar errors, identify root causes)
- `[medium]` Auto-PR creation for fixes (branch, fix, test, PR)
- `[medium]` Performance regression detection
- `[medium]` User feedback ingestion (support tickets, GitHub issues)
- `[low]` Self-improving: track which fixes worked, learn patterns
- `[low]` Multi-repo dependency impact analysis

### Integrations
- `[high]` Health check endpoints on all suite projects
- `[high]` Beacon integration for AI analysis tasks
- `[medium]` Atelier integration for complex fix orchestration
- `[medium]` Lumen integration for fix activity visibility
- `[low]` External error tracking (Sentry, etc.)

### Infrastructure
- `[high]` Supabase migration (error data, fix history)
- `[medium]` Cloud deployment (Vercel + Supabase)
- `[low]` Webhook notifications for fix proposals
