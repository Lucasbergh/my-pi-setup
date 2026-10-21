# Setup (Lucas's fork)

Fork of [davis7dotsh/my-pi-setup](https://github.com/davis7dotsh/my-pi-setup). Changes from upstream:

- Installed as a **pi package** (`pi install`), not cloned over `~/.pi/agent`.
- pi packages are `peerDependencies` (pi 1.3 supplies them at runtime).
- Subagents: Claude Agent SDK and Codex backends removed — pi harness only.
- Summaries default to `anthropic/claude-haiku-5-5` instead of `openai-codex`.
- `spark-strict-tools` removed (upstream's private provider).
- **API keys only.** No Claude or ChatGPT subscription is used by pi.

## Install

```sh
pi install https://github.com/Lucasbergh/my-pi-setup
```

## Keys

Model providers — run inside pi, stored in `~/.pi/agent/auth.json`:

```
/login anthropic     # Anthropic Console API key
/login openrouter    # OpenRouter key (cheap models, Jev)
```

Firecrawl — `~/.pi/agent/.env` (see `.env.example`):

```
FIRECRAWL_API_KEY=fc-...
```

## Theme

`~/.pi/agent/settings.json`:

```json
{ "theme": "github-dark-default" }
```

## fd and rg

`file-search` uses system `fd`/`rg` or `~/.pi/agent/bin/`. Both already exist there on this machine.
