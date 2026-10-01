# Copilot customizations

Copilot plugin rules for contextual questions and long-running tasks.

Before asking questions, the contextual-questions rule gives enough context to make an
informed choice. Before asking, it states the problem, outlines meaningful
solutions and their pros and cons, and makes a recommendation when
appropriate. The rule covers ordinary questions and Superpowers workflows
when the client attaches it. Simple questions stay concise.

The long-running-tasks rule prefers synchronous execution for one-shot
commands. If a command is detached, the agent records its execution ID,
expected result, and next action. When invoked after completion, it reads
the final output, checks the result, and resumes the original request
without a separate "continue" message.

Instructions cannot make VS Code wake an agent or deliver a missing
completion notification. They guide continuation when the agent is
invoked; client support for notifications is still required.

## Install

In Copilot CLI:

```text
copilot plugin install Blackhex/copilot-customizations
```

In VS Code, install the plugin from its GitHub repository through the
Copilot plugin interface. The rules can be applied when a client supports
plugin rules and the plugin is installed and enabled; no custom agent
selection or skill invocation is required. File-matched instructions
may not apply to questions without an associated file.

To use an editable local checkout directly in VS Code, add its absolute
path to your **user** `settings.json` instead of installing a cached copy:

```json
"chat.pluginLocations": {
  "C:\\Projekty\\copilot-customizations": true
}
```

VS Code watches plugin rule directories and the manifest in this
configuration, so changes in the checkout can be picked up without
reinstalling. Start a new chat to use updated instructions in a
conversation; an existing chat may retain its earlier context. For
Copilot CLI, use `copilot --plugin-dir C:\Projekty\copilot-customizations`
to load the working tree for that invocation.

## Verify

```text
copilot plugin list
copilot instruction list
```

Confirm that `copilot-customizations` is installed. In a fresh
interactive Copilot CLI session, use `/env` to inspect the loaded
environment and `/instructions` to inspect available instruction
sources. Plugin installation alone does not prove the rules were attached
to a particular request. `copilot instruction list` may omit
plugin-contributed rules depending on client settings and file context.

To update the cached installation after a repository change, run
`copilot plugin install Blackhex/copilot-customizations` again.
