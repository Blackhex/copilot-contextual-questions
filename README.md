# Contextual questions for Copilot

An always-active Copilot plugin rule that asks questions with enough
context to make an informed choice. Before asking, it states the problem,
outlines meaningful solutions and their pros and cons, and makes a
recommendation when appropriate. It applies to ordinary questions and
Superpowers workflows alike. Simple questions stay concise.

## Install

In Copilot CLI:

```text
copilot plugin install Blackhex/copilot-contextual-questions
```

In VS Code, install the plugin from its GitHub repository through the
Copilot plugin interface. The rule applies when a client supports plugin
rules and the plugin is installed and enabled; no custom agent selection
or skill invocation is required.

## Verify

```text
copilot plugin list
copilot instruction list
```

Confirm that `copilot-contextual-questions` is installed and that
`contextual-questions.instructions.md` appears among the discovered
instructions. Start a new session to pick up the newly installed rule.

To update the cached installation after a repository change, run
`copilot plugin install Blackhex/copilot-contextual-questions` again.
