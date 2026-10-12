# Simple Harness maintenance

Keep exactly four skills: checkpoint, sync, tidy-docs, verify. Self-review lives in
`templates/AGENTS.md`; verify checks behavior by running it, never by asking the user to read code.
Minimize always-loaded context: the guidance block and skill descriptions load in
every session, so keep them short. verify uses whatever browser tool the user installed
and never installs one; the plugin ships no MCP server.
Behavior lives under `plugins/simple-harness/`; consuming projects own their docs.
Support Codex and Claude with the same skill sources. Keep instructions brief,
language-agnostic, and suitable for users who delegate all coding to an agent.
Most users work on Windows: no shell scripts; setup uses the agent's file tools.
Do not add a runner, hooks, MCP servers, model pins, or dependencies without a request.
The document budget is defined once in `templates/AGENTS.md`; skills point to it.
Only an explicit setup request creates files in a project.

Validate with `claude plugin validate . --strict` and
`claude plugin validate plugins/simple-harness --strict`.
All manifests must agree on name, version, and description; bump the version on
every release. Setup changes must preserve existing content and be idempotent:
request setup twice in a temporary project with Claude and with Codex
(temporary `CODEX_HOME`, `codex plugin marketplace add .`).
