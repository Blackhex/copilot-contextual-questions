# Contextual questions Copilot plugin

## Goal

When asking the user a question, explain the problem and relevant context,
present viable options with their benefits and drawbacks, then ask one
focused question. This applies to all questions, especially those asked
during Superpowers workflows.

## Packaging and behavior

Publish a public Agent Plugins 1.0 repository named
`Blackhex/copilot-contextual-questions`. Include a manifest and one
Copilot-specific rule under `com.github.copilot/rules/`. The rule is
always active when the installed plugin's rules are loaded: it does not
require selecting a custom agent or invoking a skill. Use concise context
for simple questions, and do not fabricate alternatives when none are
meaningful. Preserve a single focused question per interaction.

## Distribution and verification

Document how to install the plugin locally and from its public repository,
how to check that the rule is loaded, and how to update an installation.
Install the plugin locally and verify the client reports the rule; verify
the repository is public after publishing. Plugin availability depends on
the Copilot client supporting plugin rules and the plugin being installed
and enabled; the plugin does not modify other installed plugins.

## Alternatives considered

- An on-demand skill is portable but may not activate for ordinary
  questions, so it does not reliably enforce this preference.
- A custom agent contains instructions only when explicitly selected,
  so ordinary questions would not be covered.
- A repository instruction file is automatically available in one
  workspace but does not carry the preference across projects.
