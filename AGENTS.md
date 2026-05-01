# AGENTS.md — AI agent guide for this repo

Purpose: concise, actionable guidance for AI coding agents working in this repository.

Quick summary
- This is a tiny Node.js notifier that exposes a CLI and a GitHub Action to send Brevo emails/SMS.

Key files
- [action.yml](action.yml): GitHub Action entrypoint used by other workflows.
- [send-alert.js](send-alert.js): Primary implementation — CLI + action runtime.
- [package.json](package.json): Node project metadata and `start` script.
- [README.md](README.md): Usage, environment variables, and example configuration.

Run & test (agent checklist)
- Use Node >=22 locally (README notes native `fetch` usage).
- Install: `npm ci`
- Run CLI: `npm start` (ensure env vars per README).
- To exercise the action locally, run the script with the same env inputs used by the action.

Agent guidance / notes
- Link, don't duplicate: prefer linking to [README.md](README.md) for env details and config examples.
- Pitfall: `action.yml` currently uses `runs.using: 'node16'` while the code uses global `fetch` (README recommends Node >=22). Before changing code or publishing releases, verify runtime compatibility or update `action.yml` to a newer Node runtime.
- Conventions: this repo is delivery-only (keep quota-checking and complex logic in the caller repo).

Suggested next customizations for agents
- Optionally add `.github/copilot-instructions.md` that references this file and highlights the Node runtime mismatch.
- Add a tiny test harness or example invocation under `.github/` for easier CI verification.

If you want, I can also create the `.github/copilot-instructions.md` now (it would simply reference this file and highlight the runtime note).
