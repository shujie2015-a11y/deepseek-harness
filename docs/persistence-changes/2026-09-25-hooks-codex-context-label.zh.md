---
description: "记录持久化类型更改及其兼容性确认。"
kind: persistence-change
---

# 2026-09-25-hooks-codex-context-label

[English](2026-09-25-hooks-codex-context-label.md) | 中文

## 概述

给持久化的 `hooks-codex` 上下文消息来源增加可选的 `label`，让部署可以给它注入的行命名。

## 目录

- [声明](#declaration)
- [兼容性](#compatibility)
- [验证](#verification)
- [开发备注](#dev-note)

<a id="declaration"></a>
## 声明

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
## 兼容性

已有日志仍然有效：只有配置了新的 `contextLabel` 时桥接才写入 `label`，其余挂载保持原来的 `{ kind: 'hooks-codex' }` 来源。该字段是附加且可选的；不读取它的消费者按生产者 kind 回落，旧记录回放行为不变。

<a id="verification"></a>
## 验证

pnpm exec vitest run packages/hooks/hooks-codex/tests：61 个测试通过。packages/client/ui-trajectory/tests/event-projection.client.spec.ts：5 个通过。packages/ui/tui/tests/tui.spec.ts：207 个通过。

<a id="dev-note"></a>
## 开发备注

无。
