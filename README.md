# Contextual questions for Copilot

Copilot plugin rule that asks questions with enough context to make an
informed choice. Before asking, it states the problem,
outlines meaningful solutions and their pros and cons, and makes a
recommendation when appropriate. It applies to ordinary questions and
Superpowers workflows alike. Simple questions stay concise.

## Install

In Copilot CLI:

```text
copilot plugin install Blackhex/copilot-contextual-questions
```

In VS Code, install the plugin from its GitHub repository through the
Copilot plugin interface. The rule can be applied when a client supports
plugin rules and the plugin is installed and enabled; no custom agent
selection or skill invocation is required. File-matched instructions
may not apply to questions without an associated file. For a reliably
always-loaded personal preference across workspaces, put the rule's
text in `$HOME/.copilot/copilot-instructions.md` as well.

## Verify

```text
copilot plugin list
copilot instruction list
```

Confirm that `copilot-contextual-questions` is installed. In a fresh
interactive Copilot CLI session, use `/env` to inspect the loaded
environment and `/instructions` to inspect available instruction
sources. Plugin installation alone does not prove the rule was attached
to a particular question. `copilot instruction list` may omit
plugin-contributed rules depending on client settings and file context.

To update the cached installation after a repository change, run
`copilot plugin install Blackhex/copilot-contextual-questions` again.
