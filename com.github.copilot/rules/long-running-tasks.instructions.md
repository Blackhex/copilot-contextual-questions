---
applyTo: "**"
description: Handle long-running tasks, hidden or background terminals, and command-completion notifications without abandoning pending work.
---

# Finish long-running tasks

- For one-shot builds, tests, installs, downloads, and scripts, use the
  terminal tool's synchronous or foreground mode and let it wait for
  completion. Avoid short timeouts that detach the command. Reserve
  background mode for persistent servers, watchers, and daemons.
- If a one-shot command moves to a background terminal or times out,
  treat it as pending, not complete. Record its terminal or execution ID,
  original goal, expected result or receipt, and next action in the
  status update. Keep this handoff available across context compaction.
- On the next agent invocation, including a command-completion
  notification or a status question, handle the pending handoff first.
  When completion is reported, retrieve the command's final output and
  exit code with the appropriate terminal tool, inspect any expected
  receipt, and continue the original request without requiring a separate
  "continue" message. Respect any newer user instruction to pause,
  cancel, or redirect the task.
- If the command failed, address the failure within the authorized scope
  and rerun the relevant check, or explain the actual blocker. Starting a
  command, silence, or an intermediate output snapshot is not evidence
  that the task succeeded. Do not relaunch a command that is still active.
- While a command is still running, follow the tool's waiting rules:
  do not poll or sleep to wait for completion. If the tool requires the
  turn to end while waiting, clearly report the pending command and next
  action; do not describe the request as finished. A synchronous command
  that already returned its full result needs no background-output lookup.
- Do not stop at reporting that a completed command finished. Continue
  the remaining work and verification until the request is resolved or
  genuinely blocked, unless the user explicitly stops or changes it.

These instructions govern continuation when the agent is invoked. They
cannot make VS Code deliver a missing completion notification or wake a
stopped agent by themselves.