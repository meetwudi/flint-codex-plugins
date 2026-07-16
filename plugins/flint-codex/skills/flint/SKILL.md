---
name: flint
description: Use when the user asks Codex to work with Flint, governed organizational knowledge, Libraries, Routines, Memory, Semantic Index discovery, or governed knowledge changes through the bundled Flint MCP server.
---

# Flint for Codex

Use the bundled `flint` MCP server as the live authority for Flint knowledge and
tools.

1. Start with `flint_intro`.
2. Follow the server instructions returned during MCP initialization.
3. Use `semantic_index_manifest` and read its actor-visible entry points before
   focused discovery.
4. Use Librarian tools for exact resource reads and governed changes; do not
   infer exact contents from Semantic Index results.
5. Respect OAuth organization scope, tool annotations, approval requirements,
   and change-set workflows supplied by Flint.
6. Re-read changed resources before claiming that a write succeeded.

If the Flint tools are unavailable, tell the user that the plugin must be
installed, authenticated, and loaded in a new Codex task. Do not silently fall
back to repository files or another knowledge source.
