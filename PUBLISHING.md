# Publishing Flint for Codex

The canonical distributable plugin lives at `plugins/flint-codex/`. The public
marketplace catalog lives at `.agents/plugins/marketplace.json`.

The Flint MCP harness in `meetwudi/meta-harness` owns the product requirement,
production endpoint, compatibility expectations, and release contract. This
repository owns the installable Codex wrapper.

## Release workflow

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

Consumers receive the release after refreshing the `flint-codex` marketplace
and reinstalling `flint-codex`. Existing tasks retain the plugin snapshot they
started with; verify the update in a new task.
