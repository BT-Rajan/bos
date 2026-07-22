# 08 - AI Behaviour

## Provider Model

A single `AIProvider` interface implemented per provider (Claude, DeepSeek, future additions). Adding a provider is one new class; nothing else in the system changes.

## Config, Not Code

Enable/disable, default provider, per-module override, timeout, max tokens, temperature, cache duration, and prompt templates are all rows in `ai_config`, editable from Admin — never hardcoded.

## Standard Response Envelope

Every provider returns: `summary`, `details`, `confidence`, `suggested_actions`. The frontend AI drawer never branches on which provider answered.

## Hard Boundaries

- The AI module has **no write access** to Projects, Contracts, Government Submissions, or Documents — read-only context in, suggestions out. Enforced at the permissions layer, not just by convention.
- The AI module never receives passwords, API keys, or full user records — only the specific business content a given request needs.
- On provider failure/timeout, the system returns a clean "AI unavailable, retry" response — the rest of the app must keep functioning; AI is never a dependency in a critical path.

## Caching & History

- Cache key: hash(provider, model, prompt, context). Redis-backed, TTL from config.
- Every call — prompt, response, provider, user, timestamp — logged to `AIHistory`, read-only, visible in Admin.

## Integration Points

Documents (summarize/extract), Contracts (draft/rewrite/summarize), Government Submissions (form-fill assistance), Customer Communication (drafting replies), Reports (executive summaries).
