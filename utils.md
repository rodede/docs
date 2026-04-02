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

## Claude

### How I use Claude Code (Meta Staff Engineer Tips)

YT https://www.youtube.com/watch?v=mZzhfPle9QU

- run in root directory -> `/init` (first time, create `CLAUDE.md`) - have build/test instructions
- `/memory` -> what the core rules are in the current context
- keyboard shortcuts:
1. **Shift+Tab** - cycles Norma,Auto-accept and Plan mode
2. **Escape** - interrupts
3. **Double Escape** - empty
- `/` commands:
1. `/clear` - clear context
2. `/context` - current context
3. `/model` - switch claude model
4. `/resume` - restore context
5. `/mcp` - shows MXP status


### Levels

YT https://www.youtube.com/watch?v=Y09u_S3w2c8 

- Level 1: Plan mode
- Level 2: CLAUDE.md
- Level 3: /commands $ /skills /hooks
- Level 4: ModelContextProtocol
- Level 5: GSD plan->execute->verify
- Level 6: sub-agents
- Level 7: Ralph Loop

### Token Economy in Claude Code

SXM https://dev-ai.siriusxm.com/discovery/learning/token_economy_in_claude_code/ 

- lazy loading (skills)
- isolation (sub-agents)
- progressive discover (rules -> link)
- Use `context: fork` in your config to run the skill in a separate history, preventing detailed steps from cluttering your main chat.
- sub-agents Route simple sub-agent tasks to cheaper models (like haiku) via configuration, reserving opus and sonnet for the main brain.


### TODO

/agents