# Codex how-to

## Description
codex hints

## Table of Contents
- [Resources](#Resources)
- [Config](#Config)
- [Commands](#Commands)


## Resources
[Official page](https://developers.openai.com/codex)
Models:
- codex -m gpt-5.2-codex
- codex -m gpt-5.1-codex-max
- codex -m gpt-5.1-codex-mini

## Config
[See page](https://developers.openai.com/codex/local-config)
```
# ~/.zshrc
eval "$(codex completion zsh)"
```

```
[features]
web_search_request = true

[sandbox_workspace_write]
network_access = true

model="gpt-5.2"
```

or start with 
```
codex -m gpt-5.1-codex-mini
```

[Agents](https://developers.openai.com/codex/guides/agents-md)
[Site](https://agents.md/#examples)

## Commands
- /init - create an AGENTS.md file with instructions for Codex
- /status - show current session configuration
- /approvals - choose what Codex can do without approval
- /model - choose what model and reasoning effort to use
- /review - review any changes and find issues

```
codex exec resume --last "Fix the race conditions you found"
codex exec resume 7f9f9a2e-1b3c-4c7a-9b0e-.... "Implement the plan"
codex --image img1.png,img2.jpg "Summarize these diagrams"
```
