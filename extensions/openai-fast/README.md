# openai-fast

Enables Fast mode for OpenAI models in Pi across its `openai` and `openai-codex` providers. It applies by provider/API, not a hardcoded model-ID list; Codex requires ChatGPT OAuth.

Forked from [Diego Petrucci's pi-extensions](https://github.com/diegopetrucci/pi-extensions)—thanks for the original.

This package is standalone-only and is not auto-loaded by the `@diegopetrucci/pi-extensions` collection package. The collection uses the unified [`fast`](../fast) extension instead.

When active, the extension injects this into eligible OpenAI and Codex request payloads:

```json
{
  "service_tier": "fast"
}
```

The user-facing feature is OpenAI **Fast mode**. The extension sends the current `service_tier: "fast"` request value.

## Eligibility

Fast mode is injected for any model using `openai-codex` / `openai-codex-responses` with ChatGPT OAuth, or `openai` with the Responses or Completions API. The model ID is not checked. Existing `service_tier` values are overridden while Fast mode is on.

## Commands

```text
/fast
```

Run `/fast` to toggle Fast mode on or off for the current session/runtime. The command reports the new state in chat, and the footer shows `fast` while Fast mode is active for an eligible model.

The extension defaults to off so installing the full collection does not accidentally spend Fast-mode credits.

## Config

Optional global config:

```text
~/<pi-config-dir>/agent/extensions/openai-fast.json
```

Optional project config:

```text
<project>/<pi-config-dir>/openai-fast.json
```

Here `<pi-config-dir>` is Pi's runtime config directory name (`CONFIG_DIR_NAME`; `.pi` by default). Project config overrides global config after Pi reports that the project is trusted.

```json
{
  "enabled": false,
  "showStatus": true
}
```

- `enabled`: default Fast-mode state when there is no session override.
- `showStatus`: show a compact `fast` status when Fast mode is active for the current model.

## Install

Clone this fork, then install the standalone package directory:

```bash
pi install /path/to/pi-extensions/extensions/openai-fast
```

Reload pi after installation:

```text
/reload
```

## Notes

- OpenAI decides which models/accounts support Fast; unsupported combinations may reject the request. Fast mode has a per-token premium, and direct OpenAI API-key requests use API billing.
- The extension defaults to off; use `/fast` to toggle it for the session.
