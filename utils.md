## Spring init project
```
  spring init \
    --type=maven-project \
    --language=java \
    --boot-version=4.0.1 \
    --java-version=25 \
    --groupId=ro.dede \
    --artifactId=XXXXX \
    --name="YYYYYY " \
    --package-name=ro.dede.zzzzz \
    --dependencies=vaadin \
    AAAAAA
```

## Codex
- [Official page](https://developers.openai.com/codex)
- [Agents](https://developers.openai.com/codex/guides/agents-md)
- [Agents example](https://agents.md/#examples)
- [Config](https://developers.openai.com/codex/local-config)
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

- Commands
```
- /init - create an AGENTS.md file with instructions for Codex
- /status - show current session configuration
- /approvals - choose what Codex can do without approval
- /model - choose what model and reasoning effort to use
- /review - review any changes and find issues
- codex -m gpt-5.2-codex
```