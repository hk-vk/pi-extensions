# openai-fast

Enables Fast mode for Pi's `openai` and `openai-codex` providers.

Forked from [Diego Petrucci's pi-extensions](https://github.com/diegopetrucci/pi-extensions)—thanks for the original.

## Supported APIs

- `openai`: Responses and Completions
- `openai-codex`: Responses with ChatGPT OAuth

## Use

```bash
pi install /path/to/pi-extensions/extensions/openai-fast
```

After installing, run `/reload`, then `/fast` to toggle Fast mode for the session. It starts off by default; the footer shows `fast` when active.

## Config

Create `~/.pi/agent/extensions/openai-fast.json`:

```json
{
  "enabled": false,
  "showStatus": true
}
```
