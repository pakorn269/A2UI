# Project Guidelines

## Architecture
- This repository is a multi-language monorepo split by concern:
  - `specification/`: versioned A2UI schemas and evaluators (`v0_8`, `v0_9`, `v0_10`).
  - `renderers/`: framework implementations (`web_core`, `lit`, `react`, `angular`, `markdown`).
  - `agent_sdks/`: agent-side SDKs (`python`, `java`).
  - `samples/`: runnable end-to-end examples for agents and clients.
  - `docs/`: MkDocs documentation sources.
  - `tools/`: auxiliary development tools.
- Treat `renderers/web_core` as the shared foundation for web renderers.
- Keep spec version boundaries explicit; do not mix `v0_8`, `v0_9`, and `v0_10` APIs in one change unless migration is the goal.

## Code Style
- Follow existing style and tooling in each package instead of introducing a repo-wide formatter.
- TypeScript packages are ESM-first and generally use `moduleResolution: bundler`.
- Prefer small, focused changes and preserve public exports unless the task explicitly requires API changes.
- Keep license headers in source files that already use them.

## Build and Test
- Run commands from the relevant package directory (there is no single root build command).
- Common TypeScript package workflow:
  1. `npm install`
  2. `npm run build`
  3. `npm test` (when available)
- Important dependency order for web renderer setup:
  1. Build `renderers/web_core` first.
  2. Build `renderers/markdown/markdown-it`.
  3. Build target renderer/client (for example `renderers/lit`, then `samples/client/lit/shell`).
- Python SDK and sample agents use `uv` (not plain `pip` workflows by default).

## Conventions
- Use local `file:` dependencies as declared in package manifests; do not replace them with published versions during normal development.
- Keep generated/build output out of source edits unless the task explicitly asks for built artifacts.
- Agent and UI payloads should be treated as untrusted input; preserve validation/sanitization behavior in renderers and SDK code.
- For contributor process and project context, refer to `README.md` and `CONTRIBUTING.md`.

## Workspace Notes
- A nested instruction file exists at `tools/composer/AGENTS.md`; instructions closest to edited files take precedence.
