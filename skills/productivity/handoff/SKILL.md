---
name: handoff
description: Write a portable handoff summary while preserving decisions and pending work in the tracker or PR.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save to the temporary directory of the user's OS - not the current workspace.

Include a "suggested skills" section in the document, naming which skills the next agent should call the Skill tool for.

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.

The temporary file is a convenience summary. Preserve important decisions, pending requests, and resumption context in the existing tracker record or PR before handing it over, following the same redaction rule as the file; reference that durable record from the summary. If no suitable record exists or it cannot be updated, report the preservation gap rather than claiming a durable handoff.

If the conversation is tied to a tracker record - a Linear issue, or a Linear project when no single issue fits - add one short pointer comment there: the handoff file's path and a one-line summary. After posting, append the comment's id, URL, and record type to the handoff document. The tracker or PR remains authoritative if the file disappears or conflicts with current state.

This skill prepares context, not task execution authority. Worker starts, worktree allocation, occupancy, publication, merge, deploy, and cleanup follow the consuming harness's existing lifecycle owner and procedure. A summary or successful send is not recipient acceptance or approval of those actions.

End the handoff document with a "Before resuming or deleting this file" checklist: re-verify referenced branches, commits, PRs, and tracker status; read the owner and latest comments; check current task ownership and live sessions through the existing lifecycle procedure (`git worktree list` proves registration, not a live writer); report conflicts to the responsible owner before resuming; confirm the recipient accepted the scope and that important decisions, pending requests, and resumption context are preserved in the tracker or PR. Retain the file and pointer until the responsible owner authorizes cleanup through that procedure; this checklist grants no deletion authority.
