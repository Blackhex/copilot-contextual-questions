# Copilot customizations

Copilot plugin rule that asks questions with enough context to make an
informed choice. Before asking, it states the problem, outlines meaningful
solutions and their pros and cons, and makes a recommendation when
appropriate. The rule covers ordinary questions and Superpowers workflows
when the client attaches it. Simple questions stay concise.

## Install

In Copilot CLI:

```text
copilot plugin install Blackhex/copilot-customizations
```

In VS Code, install the plugin from its GitHub repository through the
Copilot plugin interface. The rule can be applied when a client supports
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
sources. Plugin installation alone does not prove the rule was attached
to a particular question. `copilot instruction list` may omit
plugin-contributed rules depending on client settings and file context.

To update the cached installation after a repository change, run
`copilot plugin install Blackhex/copilot-customizations` again.
