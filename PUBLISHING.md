# Publishing Flint plugins

This repository serves two agent ecosystems:

- Codex: distributable plugin at `plugins/flint-codex/`, marketplace catalog at
  `.agents/plugins/marketplace.json`.
- Claude Code: distributable plugin at `plugins/flint-claude/`, marketplace
  manifest at `.claude-plugin/marketplace.json`.

The Flint MCP harness in `meetwudi/meta-harness` owns the product requirement,
production endpoint, compatibility expectations, and release contract. This
repository owns the installable agent wrappers.

## Release workflow (Codex)

1. Confirm the production Flint MCP endpoint and OAuth flow are healthy.
2. Update the plugin skill or metadata without duplicating server-owned tool
   schemas or governed MCP instructions.
3. Bump `plugins/flint-codex/.codex-plugin/plugin.json` to a new semantic
   version.
4. Validate the plugin:

   ```bash
   python3 /path/to/plugin-creator/scripts/validate_plugin.py plugins/flint-codex
   ```

5. Test installation from the marketplace and complete OAuth.
6. In a new Codex task, call `flint_intro` and verify the reported Flint project
   Library. Ask Codex to run a governed Routine and verify that Codex acts as
   the external execution host rather than refusing because Flint has no generic
   Routine runner or host-only handoff.
7. Commit and push the release to `main`.

## Release workflow (Claude Code)

1. Confirm the production Flint MCP endpoint and OAuth flow are healthy.
2. Update the plugin skill or metadata without duplicating server-owned tool
   schemas or governed MCP instructions. Keep the `flint-claude` skill and the
   `flint-codex` skill aligned on curation and Routine boundary behavior.
3. Bump `plugins/flint-claude/.claude-plugin/plugin.json` to a new semantic
   version.
4. Test installation from the marketplace in Claude Code:

   ```text
   /plugin marketplace add meetwudi/flint-codex-plugins
   /plugin install flint-claude@flint
   ```

   Complete Flint OAuth for the bundled `flint` MCP server (via the prompt or
   `/mcp`).
5. In a new Claude Code session, call `flint_intro` and verify the reported
   Flint project Library. Ask Claude Code to run a governed Routine and verify
   that it acts as the external execution host rather than refusing because
   Flint has no generic Routine runner or host-only handoff.
6. Commit and push the release to `main`.

Consumers receive a release after refreshing the marketplace and reinstalling
the plugin (`codex plugin marketplace upgrade flint-codex` for Codex,
`/plugin marketplace update flint` for Claude Code). Existing tasks and
sessions retain the plugin snapshot they started with; verify updates in a new
task or session.
