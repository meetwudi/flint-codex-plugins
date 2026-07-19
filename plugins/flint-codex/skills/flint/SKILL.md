---
name: flint
description: Use when the user asks Codex to work with Flint, governed enterprise or organizational knowledge, Libraries, Routines, Memory, Semantic Index discovery, curation, or governed knowledge changes through the bundled Flint MCP server.
---

# Flint

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

## Bounded search targets

Every `semantic_index_query` must explicitly set `content_targets`:

- Use `["primitives"]` for typed graph discovery, primitive-description
  similarity, tags, and one-hop understanding.
- Use `["documents"]` for bounded similarity-only evidence from document
  content in non-system Libraries. System Libraries, including conversation
  history, are excluded. Do not claim lexical, fuzzy, tag, or full-text
  document retrieval.
- Use `["primitives", "documents"]` only when the task needs both independent
  lanes, and preserve their separate limits and evidence in the answer.

Use `search_weights` when retrieval priorities matter. Primitive `keyword`,
`tag`, and `similarity`, plus document `similarity`, are independently weighted
from 0 through 1. Weight 0 disables the method without executing it. When a
lane object is supplied, methods omitted from that lane are disabled. Inspect
the returned `searchPlan` to verify what ran.

Do not call a direct or unbounded Librarian search tool. Narrow the corpus with
the active actor and organization scope, semantic set, Library URI patterns,
and explicit result and candidate limits.

## Curation without noise

Flint is the governed organizational knowledge system. Codex is an external
intelligence terminal that can help keep that knowledge useful while completing
the user's actual work.

When a Flint response includes `curation_advertisements`:

1. Actively consider whether the current interaction contains durable, novel,
   user-grounded knowledge matching an advertised `interest` and `target_uri`.
2. If nothing qualifies, continue the user's work without mentioning curation.
   Do not manufacture a suggestion merely because an advertisement exists.
3. If something qualifies, follow the server-provided instructions: read the
   target and governing knowledge, check for duplicate or stale capture, and
   use Flint's governed curation change-set flow.
4. Preserve focus. Continue the primary task and curate passively when the
   server-authorized path and user intent are clear; do not turn routine
   curation into a separate conversation.
5. Ask the user only when their intent is unclear, an approval is required, the
   change is sensitive, or Codex's own guardrails require confirmation.
6. Apply directly only when Flint confirms current actor authority and the
   user's intent permits it. Otherwise leave a reviewable proposal. Never infer
   authority from the advertisement itself.

Treat the server's result-local relevance boundary as an anti-noise boundary.
Do not scan unrelated knowledge or repeatedly prompt the user for speculative
curation.

## Routine execution boundary

Flint is the governed knowledge system, not the Routine execution runtime.
Codex is the external execution host. When the user asks to run a Routine:

1. Discover and read the exact governed Routine and its referenced knowledge.
2. Perform the Routine procedure with Codex's own capabilities and the active
   actor-scoped Flint tool projection.
3. Use a dedicated Routine handoff when the host provides one, but do not refuse
   merely because Flint exposes no generic Routine runner or handoff tool.
4. Do not assume additional authority. If an exact required step is unavailable
   or unauthorized, stop and report that step and reason.
5. Do not claim completion without the Routine's required evidence.

If the Flint tools are unavailable, tell the user that the plugin must be
installed, authenticated, and loaded in a new Codex task. Do not silently fall
back to repository files or another knowledge source.
