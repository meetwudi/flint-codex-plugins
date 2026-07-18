# Flint

Flint is the public plugin marketplace for Flint, a governed enterprise and
organizational knowledge system. It serves both Codex and Claude Code. Each
plugin connects the agent to the production Flint MCP server through OAuth and
adds a thin skill for discovering, using, and curating shared knowledge.

## Install (Codex)

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

## Install (Claude Code)

Add the same repository as a Claude Code marketplace and install the plugin:

```text
/plugin marketplace add meetwudi/flint-codex-plugins
/plugin install flint-claude@flint
```

Authenticate the bundled `flint` MCP server when prompted, or run `/mcp` and
complete the Flint OAuth flow, selecting the organization that the connection
should use. Then start a new Claude Code session so the plugin's MCP server and
skill are loaded.

## Verify

In a new task or session, ask:

```text
Use Flint. Call flint_intro and tell me which project Library it reports.
```

To verify the Routine boundary, ask the agent to run a governed Routine. The
agent should discover and follow the Routine itself; it should not wait for or
claim that Flint needs to expose a generic Routine runner.

The production Flint MCP endpoint is:

```text
https://flint.craftgarden.io/mcp
```

The endpoint, OAuth flow, server instructions, tool schemas, organization
scope, and governed knowledge remain owned by Flint production. This repository
contains only the agent distribution wrappers; it contains no Flint credentials
or customer knowledge.

## Curation while you work

The agent treats Flint's curation advertisements as quiet, request-local
signals. It considers whether the current work produced durable, novel
knowledge for an advertised destination, ignores non-matches without
interrupting the user, and uses Flint's governed curation flow when something
qualifies. Depending on the actor's authority and the user's intent, that can
be a direct application or a reviewable proposal. The agent asks only when
approval, ambiguity, sensitivity, or its own guardrails require it, so curation
supports the work instead of becoming the work.

## Update an installed plugin

Publishing a new plugin version makes it available to downstream users, but it
does not silently replace an installed cached copy.

Codex:

```bash
codex plugin marketplace upgrade flint-codex
codex plugin add flint-codex@flint-codex
```

Claude Code:

```text
/plugin marketplace update flint
/plugin install flint-claude@flint
```

Then start a new task or session.

## Publishing

See [PUBLISHING.md](PUBLISHING.md) for the maintainer release workflow. The
source-of-truth publication contract is governed by the Flint MCP harness in
the `meetwudi/meta-harness` repository.
