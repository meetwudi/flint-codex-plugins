# Flint

Flint is the public Codex plugin marketplace for Flint. The plugin
connects Codex to the production Flint MCP server through OAuth and adds a thin
skill that helps Codex begin governed knowledge discovery.

## Install

Add the public marketplace and install the plugin:

```bash
codex plugin marketplace add meetwudi/flint-codex-plugins
codex plugin add flint-codex@flint-codex
```

Complete the Flint OAuth flow when prompted and select the organization that
the connection should use. Then start a new Codex task so the plugin's MCP
server and skill are loaded.

If Codex does not prompt for authentication during installation, run:

```bash
codex mcp login flint
```

## Verify

In a new Codex task, ask:

```text
Use Flint. Call flint_intro and tell me which project Library it reports.
```

To verify the Routine boundary, ask Codex to run a governed Routine. Codex
should discover and follow the Routine itself; it should not wait for or claim
that Flint needs to expose a generic Routine runner.

The production Flint MCP endpoint is:

```text
https://flint-839963098585.us-east1.run.app/mcp
```

The endpoint, OAuth flow, server instructions, tool schemas, organization
scope, and governed knowledge remain owned by Flint production. This repository
contains only the Codex distribution wrapper; it contains no Flint credentials
or customer knowledge.

## Update an installed plugin

Publishing a new plugin version makes it available to downstream users, but it
does not silently replace an installed cached copy. Refresh the marketplace,
reinstall the plugin, and start a new task:

```bash
codex plugin marketplace upgrade flint-codex
codex plugin add flint-codex@flint-codex
```

## Publishing

See [PUBLISHING.md](PUBLISHING.md) for the maintainer release workflow. The
source-of-truth publication contract is governed by the Flint MCP harness in
the `meetwudi/meta-harness` repository.
