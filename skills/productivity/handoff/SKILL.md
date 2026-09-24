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

If the conversation is tied to a tracker issue (e.g. a Linear issue), add one short comment on that issue with the handoff file's path and a one-line summary. Do not paste the handoff content into the comment - the file stays the source of truth, the comment is only a pointer so a session working from the tracker can find it. Record the exact comment id you get back.

## Resuming from a handoff

Reading a handoff file is not the same as completing it. Before deleting a handoff file or its tracker pointer comment:

1. Read the full handoff file and the artifacts it references (issue, PR, git state, worktree).
2. Re-check current state - branch, commits, issue status, existing workers - since it may have drifted since the handoff was written.
3. Confirm no other session or worker already owns the same task. Reuse the project's existing ownership/single-writer check; do not invent a new lock for handoff.
4. Fold any decision or remaining-work item that exists only in the handoff into the issue or other durable artifact.
5. Only then delete the handoff file and its tracker pointer comment, if one exists.

Record the session identifier the handoff was written from separately from the tracker issue id and any workspace/agent id used to run it - don't conflate them.
