---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save to the temporary directory of the user's OS - not the current workspace.

Include a "suggested skills" section in the document, naming which skills the next agent should call the Skill tool for.

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.

If the conversation is tied to a tracker issue or project (e.g. a Linear issue or Linear project), add one short comment there: the handoff file's path and a one-line summary, following the same redaction rule as the file. Prefer an issue when one clearly matches; use a project instead only when no single issue captures the conversation's scope but an active project does. The comment is a pointer - the file remains the source of truth. After posting, append the comment's id, URL, and which kind of record it was posted to (issue or project) to the handoff document.

End the handoff document with a "Before deleting this file" checklist for whoever picks it up: re-verify every referenced artifact (branch, commits, PR, issue/project status) against current state and note what drifted; check the issue's or project's assignee/lead, latest comments, open PRs on the branch, and `git worktree list` for another active session, and pause to ask the user if one appears; fold any handoff-only decision into the issue or project; then delete this file and the tracker comment above.
