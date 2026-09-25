---
description: "Records a persistence type transition and its compatibility acknowledgement."
kind: persistence-change
---

# 2026-09-25-hooks-codex-context-label

English | [中文](2026-09-25-hooks-codex-context-label.zh.md)

## Summary

Adds an optional `label` to the persisted `hooks-codex` context-message source, so a deployment can name the rows its hooks inject.

## Table of Contents

- [Declaration](#declaration)
- [Compatibility](#compatibility)
- [Verification](#verification)
- [Dev Note](#dev-note)

<a id="declaration"></a>
## Declaration

```yaml persistence-change
schemaVersion: 1
id: 2026-09-25-hooks-codex-context-label
baseline: false
changes:
  - root: "event:agent/inbox/spliced"
    previous: "2026-09-16-session-format-v4"
    after: "94543163be71e1634c0102757dc16e5f6a578267597cbddad29e0b2b418333fb"
    decision: same-version
  - root: "event:developer/message"
    previous: "2026-09-16-session-format-v4"
    after: "f58d66fb1ac6d542582eea02d172930f699f0da69ce9bac893ee0144b4b2e82c"
    decision: same-version
  - root: "event:session/title-llm-request"
    previous: "2026-09-16-session-format-v4"
    after: "90bf014792874c450bdad3ff831c6e25d7d98bbbad2bcdd0a4ead36b72139408"
    decision: same-version
  - root: "event:user/message"
    previous: "2026-09-16-session-format-v4"
    after: "7c41c4acc5fe2468fe21280ecba7281e3e3938038560d1636928688efddc1e73"
    decision: same-version
```

<a id="compatibility"></a>
## Compatibility

Existing logs stay valid: the bridge writes `label` only when its new `contextLabel` config is set, and every other mount keeps the previous `{ kind: 'hooks-codex' }` source. The field is additive and optional; consumers that do not read it fall back to the producer kind, and replay of older records is unchanged.

<a id="verification"></a>
## Verification

pnpm exec vitest run packages/hooks/hooks-codex/tests: 61 tests passed. packages/client/ui-trajectory/tests/event-projection.client.spec.ts: 5 passed. packages/ui/tui/tests/tui.spec.ts: 207 passed.

<a id="dev-note"></a>
## Dev Note

None.
