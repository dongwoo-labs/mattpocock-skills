---
name: diagnosing-bugs
description: Temporary T1 compatibility entry for explicitly selecting diagnose-bug deep mode on a hard bug or performance regression.
disable-model-invocation: true
---

# Diagnosing Bugs

This is a temporary T1 compatibility entry for the old name, not a second diagnosis
implementation. Invoke it only when the user explicitly requests this skill. Ordinary bug
reports and quick diagnostic questions do not select it automatically.

## Select the target explicitly

Call the Skill tool with `diagnose-bug`. In the task prompt, explicitly select deep mode
using the applicable natural-language instruction below, filling in the supplied context:

- Fix requested within existing authority: `심층 모드로 진행해줘. 기존 writer가 <환경>에서 <증상>을 재현하고, 진단·수정·회귀 검증까지 수행해줘.`
- Cause only, no fix requested or permitted: `심층 모드로 원인만 진단해줘. <증상>의 원인을 찾되 수정하지 마.`

These are task instructions, not CLI flags, a mode schema or an alias parser. Do not rely
on the target's default mode: the old-name entry explicitly selects deep mode. Pass the
original request, expected outcome, actual revision/environment, supplied code/logs/evidence,
prior attempts, reproduction command, pending work and existing permissions unchanged.
Do not reinterpret a cause-only request as permission to fix.

The consuming harness must expose the model-invoked `diagnose-bug` Skill and support this
explicit mode contract. If that Skill/frontdoor is absent, inaccessible or incompatible,
report the missing dependency and stop the dependent flow. Do not install it, invent a
successful call or fall back to a local copy of the phases.

## Preserve ownership and evidence boundaries

Follow the target's inline deep workflow and common diagnostic rules; do not duplicate
its six phases here or make the target depend on this compatibility entry. The existing
writer owns authorized reproduction, diagnosis, fixes and regression verification. Any
optional diagnostic helper is diagnose-only/no-edit, readonly, noBrowser and task-local;
it receives the target's Common diagnostic rules and may not delegate again. This is a
prompt-only contract, not enforced tool permission isolation. Preserve any caller ban on
delegation and return additional delegation needs instead of bypassing it.

Skill selection grants no new write, runtime, installation, paid-call, publication or
lifecycle authority. Cause-only requests stop at diagnosis and mark fix/regression NOT_RUN.
Missing reproduction access blocks the dependent deep loop, not independent read-only
inspection, and never earns deep acceptance PASS. Distinguish source checks, supplied
captures, live execution and scripted replay in the result.

Redact every secret before showing commands, outputs or captured artifacts: use
`<REDACTED>` and keep credentials in environment variables. If redaction removes the
needed diagnostic signal, ask for safe evidence rather than exposing the secret.
