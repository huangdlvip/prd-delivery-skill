# 上线验收标准

Use this reference when writing or reviewing section `上线验收标准`.

## Module SPEC vs Launch Acceptance

- Module-level `验收标准` in SPEC verifies a single function's behavior and should use GIVEN / WHEN / THEN.
- PRD-level `上线验收标准` verifies whether the whole requirement is ready to release, grey release, or expand traffic.
- Do not copy every SPEC acceptance case into launch acceptance. Extract only critical release gates.

## Recommended Table

```markdown
| 验收类型 | 关键验收项 | 通过标准 | 优先级 |
|---|---|---|---|
| 主流程 |  |  | P0 |
| 异常流程 |  |  | P0 |
| 权限 |  |  | P1 |
| 数据 |  |  | P0 |
| 埋点 |  |  | P1 |
| 发布命中 |  |  | P0 |
```

## Writing Guidance

- 主流程：the core user/business path can complete end to end.
- 异常流程：the highest-risk failures are handled without broken state or silent failure.
- 权限：role, package, grey-list, or user-scope behavior is correct.
- 数据：created, updated, queried, synced, or displayed data matches the expected source and state.
- 埋点：required events are emitted with required fields and can support the intended observation or analysis.
- 发布命中：grey/A/B/full-release hit rules behave as planned.

Good acceptance items are short, observable, and release-gating. Avoid `功能正常`, `页面正常`, or `数据正常`.
