# qa-kit

A small Claude Code plugin for checking your work before you open a pull request. It adds one slash command and one subagent.

## What's inside

| Component | Type | What it does |
|---|---|---|
| `summarize-changes` | Slash command | Lists every file touched on the current branch with a one-line description of each change — short enough to paste into a PR description. |
| `code-reviewer` | Subagent | Reviews recent changes for bugs, missing error handling and unclear names, and returns a short list grouped by severity (high, medium, low). |

## Structure

```
.
├── .claude-plugin/
│   └── plugin.json            # manifest: name + version
├── commands/
│   └── summarize-changes.md
├── agents/
│   └── code-reviewer.md
└── README.md
```

## How to use it

1. From the repo root, start Claude Code with the plugin loaded:

   ```bash
   claude --plugin-dir .
   ```

2. **Summarise your branch** — run the command by its namespaced name:

   ```
   /qa-kit:summarize-changes
   ```

3. **Get a code review** — just ask, for example:

   ```
   Review my recent changes.
   ```

   Claude will hand the task to the `code-reviewer` subagent, which reads the changed files (it only has `Read`, `Grep` and `Glob`, so it can't edit anything) and reports back.

4. After editing any plugin file, run `/reload-plugins` to pick up the changes.

## Version

0.1.0
