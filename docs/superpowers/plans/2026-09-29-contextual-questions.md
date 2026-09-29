# Contextual Questions Plugin Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish and install a public Copilot plugin that supplies context, choices, and trade-offs whenever the assistant asks a question.

**Architecture:** An Agent Plugins 1.0 manifest identifies the package. One Copilot-specific rule is automatically loaded by compatible clients. A README documents direct installation, inspection, and updates.

**Tech Stack:** Agent Plugins 1.0, Copilot rules (Markdown), Git, GitHub CLI.

## Global Constraints

- Repository: `Blackhex/copilot-contextual-questions` (public).
- Apply to all questions, especially Superpowers workflows.
- Give the problem, relevant context, meaningful solutions, and each solution's pros and cons; ask one focused question.
- Keep trivial questions concise and never invent alternatives.
- Do not modify other installed plugins.

---

### Task 1: Package and publish the instruction

**Files:**
- Create: `plugin.json`
- Create: `com.github.copilot/rules/contextual-questions.instructions.md`
- Create: `README.md`

**Interfaces:**
- Consumes: Copilot Agent Plugins 1.0 discovery of `com.github.copilot/rules/`.
- Produces: a directly installable plugin exposing one global Copilot instruction.

- [ ] **Step 1: Establish pre-install absence**

Run: `copilot instruction list` and `copilot plugin list`.
Expected: Neither command lists `contextual-questions.instructions.md` or `copilot-contextual-questions`.

- [ ] **Step 2: Create the manifest and rule**

`plugin.json`:

```json
{
  "$schema": "https://agent-plugins.org/schemas/1.0.0/plugin.schema.json",
  "name": "copilot-contextual-questions",
  "version": "1.0.0",
  "description": "Give context and trade-offs before asking the user questions."
}
```

`com.github.copilot/rules/contextual-questions.instructions.md`:

```markdown
# Ask contextual questions

Whenever you ask the user a question, first explain the problem and the
relevant context. Present meaningful possible solutions and the pros and
cons of each, including your recommendation when one is justified. Then
ask one clear, focused question. This applies to every question,
especially during Superpowers workflows and when using a question tool.
For straightforward questions, keep the explanation proportionate; do
not manufacture choices or trade-offs that do not exist.
```

- [ ] **Step 3: Document installation and verification**

Create `README.md` with the rule's behavior and commands:

```text
copilot plugin install Blackhex/copilot-contextual-questions
copilot plugin list
copilot instruction list
```

Explain that the instruction appears only after installing/enabling the
plugin in a client supporting plugin rules. Re-run `copilot plugin install
Blackhex/copilot-contextual-questions` after publishing updates because
installed components are cached.

- [ ] **Step 4: Validate locally**

Run JSON parsing (`python -m json.tool plugin.json`), inspect the rule
through `copilot instruction list` after local installation if available,
and check `git status --short`. Expected: valid JSON and discovered rule.
If direct local installation is not supported by this CLI, publish
first, install via `owner/repo`, then inspect instruction discovery.

- [ ] **Step 5: Commit and publish**

Commit these three files with `feat: add contextual question plugin` and
the repository's Co-authored-by trailer. Use `gh repo create
Blackhex/copilot-contextual-questions --public --source . --remote
origin --push` from the plugin repository. Confirm its public visibility.

- [ ] **Step 6: Install and confirm**

Run `copilot plugin install Blackhex/copilot-contextual-questions`,
`copilot plugin list`, and `copilot instruction list`. Expected: the
plugin is enabled and the instruction is discovered. If the CLI does
not show the rule, diagnose its format and retry before claiming success.
