# 发布计划

Use this reference when the PRD involves full release, grey release, A/B testing, rollout, rollback, operations collaboration, business monitoring, or running quality.

## Minimum Fields

```markdown
- 发布方式：全量 / 灰度 / A/B
- 全量：完成上线验收即可，不展开后续放量或实验计划
- 灰度：写清楚命中规则、放量计划、观测信号、暂停/回滚信号
- A/B：写清楚实验方案、分组规则、观测信号、选择计划
- 协同运营事项：
```

## Guidance

- 全量：only write the release method and any necessary operations/customer-service sync. Do not add rollout, experiment, or observation-plan fields unless they are truly needed.
- 灰度：explain hit population, rollout cadence, observation signals, pause/rollback signals, and expansion criteria.
- A/B：explain experiment scheme, control/experiment groups, randomization or hit rule, observation signals, and selection plan.
- 暂停/回滚信号：write concrete thresholds, events, or user/business symptoms, not generic `异常时回滚`.
- 协同运营事项：include sales, operations, customer service, user notification, help center, or pricing/rights wording when relevant.
