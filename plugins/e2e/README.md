# e2e by TesterArmy

[e2e](https://tester.army/e2e) is an open source end-to-end testing framework
for web and mobile apps. A test mixes agent goals (`agent.act`) with exact
locator steps and assertions, and runs in a browser or on an iOS simulator,
Android emulator, or phone.

## Skills

- **e2e**: set up e2e in a project, write and fix tests, run them, debug a
  failed run, drive the running app over the e2e MCP server, explore an app
  toward a goal, and bug bash a branch with each bug proven by a repro test.
- **create-verification-skill**: generate a project-local `verify-<app>`
  skill and feature map on top of e2e. Invoke it with
  `$e2e:create-verification-skill`; it never loads on its own.

## Requirements

Node.js 24.8 or newer, or 22.22.3 or newer on Node.js 22. In a project that
does not use e2e yet, the skill asks before setting it up. Agent steps need a
model: an AI SDK provider key, or a ChatGPT subscription through
`npx e2e login openai`.

## MCP server

The plugin does not bundle the e2e MCP server, which runs from the project's
own `e2e` install. To let Codex drive the running app, add it to the
project's `.codex/config.toml`; the skill does this with your approval:

```toml
[mcp_servers.e2e]
command = "npx"
args = ["--no", "e2e", "mcp"]
```

## Data

- The e2e CLI sends anonymous usage telemetry (commands, engines, versions,
  failure codes; never test content, app content, or credentials) to a
  PostHog project run by the e2e maintainers. Turn it off with
  `E2E_TELEMETRY_DISABLED=1`, `DO_NOT_TRACK=1`, or `npx e2e telemetry disable`.
  See [Telemetry](https://e2e.tester.army/docs/telemetry).
- `npx e2e feedback` sends a report to the same project. The skill shows the
  report first and sends it only when you agree.
- Agent steps send the redacted screen to the model provider you configure.
  Secrets never reach the model.

## Source

The skills are adapted from
[tester-army/e2e](https://github.com/tester-army/e2e) (`skills/`) for Codex:
per-project MCP setup, and asking before setting e2e up or sending feedback.
Docs: <https://e2e.tester.army/docs>.
