---
name: prd-delivery
description: 中文交付型 PRD 创建、评审、需求拆解和研发友好化 Skill。Use when the user needs to write or review PRDs in Chinese for Git codebase collaboration, frontend-page-as-prototype workflows, AI Coding handoff, SPEC-style functional requirements, launch acceptance, release planning, grey release, A/B testing, commercialization, risk management, business monitoring, running quality, or project context enrichment from authorized workflow/context Skills.
---

# PRD Delivery

## Overview

Use this skill to help product owners create, review, and refine Chinese delivery-oriented PRDs for fast product-engineering collaboration. Treat the frontend page as the source of truth for visual design; make the PRD responsible for product scheme, functional SPEC, data tracking, launch acceptance, release plan, commercialization, and key risks that affect launch or business running quality.

Default PRD filename: `{需求名称}_PRD.md`.

## Capabilities

1. 从 0 到 1 写 PRD：基于业务想法、产品假设、前端页面、会议纪要或用户描述，先分阶段确认待确认项、产品方案和功能需求清单，再生成中文交付型 PRD。
2. PRD 评审：检查 PRD 是否覆盖产品方案、功能 SPEC、数据埋点、上线验收、发布计划、商业化、风险依赖，以及是否存在需要先向用户确认的关键问题。
3. 需求拆解：将模糊需求拆成功能需求清单、功能模块、SPEC 功能描述、上线验收标准和发布计划。
4. 产品方案推演：围绕面向用户、问题场景、解决方案、本期范围、不做范围、后续迭代和关键取舍推演产品方案。
5. 研发友好化 / AI Coding 友好化：将自然语言需求改写成可实现、可测试、可交给 Agent 执行的 SPEC。
6. 上线与验证：补齐发布策略、灰度/A/B 观测信号、放量/暂停/下架/回滚标准和协同运营事项。
7. 前端设计反向校验：在交互输出中提示影响实现、验收或上线的前端页面缺口，不写入 PRD 正文。
8. 项目上下文增强：当安装并授权项目上下文类 Skill（如 `bi-workflow-agent`）时，使用其补充相关项目的系统逻辑、线上数据库、关键日志和线上运行数据，让产品方案和功能需求更贴合真实项目迭代。

## Workflow

1. Read the user request and available codebase context. If the user points to files, pages, branches, PRs, or existing docs, inspect them before writing.
2. If an authorized project-context Skill is installed and the requirement would benefit from real project context, use it as context enrichment before product-scheme exploration. For `bi-workflow-agent`, follow that Skill's own instructions: fetch its `context` once, confirm available authorized capabilities, and use relevant subagents to understand system logic, online data, key logs, or running behavior across authorized projects. Do not start cloud development workspaces unless the user explicitly asks for cloud engineering development.
3. When an uncertainty can be checked from codebase, existing interfaces, fields, metric definitions, online read-only database, key logs, or user behavior data through available project context, check it first. Do not ask the product owner whether to use project context, and do not list discoverable project facts as `待确认问题` before checking.
4. Identify whether the task is writing a new PRD, reviewing an existing PRD, decomposing requirements, refining a product scheme, converting text to SPEC, or completing release validation.
5. Before writing a PRD, run the staged PRD gate: first clarify blocking questions, then co-create and confirm the product scheme, then confirm the feature list. Do not combine these decisions into one large output.
6. If critical information is missing after codebase/project-context checks, ask only the remaining blocking confirmation questions first. Do not output product scheme, feature list, PRD正文, module SPEC, acceptance standards, or release plan in the same turn.
7. After blocking questions are resolved, output the product scheme for discussion and confirmation. Stop and wait for the product owner to confirm or adjust.
8. After the product scheme reaches consensus, output the feature requirement list for confirmation. Stop and wait for the product owner to confirm or adjust.
9. After both the product scheme and feature list are confirmed, perform a frontend design reverse check before writing the PRD. Output `前端设计待补齐` only when page states or interaction details are missing; if none are found, say so briefly.
10. Only after the product owner handles blocking frontend design gaps, write the PRD using `assets/prd-template.md` as an architecture reference, not a fixed form. Adjust sections and content to the actual requirement.
11. For each functional module, use SPEC-style writing. Read `references/spec-writing.md` when writing or converting functional requirements.
12. For launch-level acceptance, read `references/acceptance-standards.md`.
13. For grey release, A/B testing, full release, release metrics, rollout, rollback, or operations collaboration, read `references/release-plan.md`.

## Pre-Writing Confirmation

Ask the user before writing when any critical item is unclear:

- 需求背景、目标、面向用户、问题场景或产品方案。
- 本期做什么、不做什么、后续迭代计划或关键取舍。
- 前端页面路径、页面位置, or how the function maps to the existing frontend page.
- Functional rules, permissions, state transitions, data source, input/output, or edge cases.
- Existing project capabilities that should be reused, if any. Decide what to reuse from the actual requirement and project context; do not force fixed categories.
- Data tracking events, tracking fields, usage purpose, or success indicators.
- Release method, hit rules, grey/A/B observation signals, rollout/pause/offline/rollback standards, or operations collaboration.
- Commercialization rules, if the requirement affects commercialization.
Use concise questions and group them by decision impact. Do not ask about every empty template field. Do not ask the product owner to confirm facts that can be reasonably checked through the codebase or authorized project-context Skill first.

## Staged PRD Gate

This gate is mandatory before creating a PRD body. Keep each interaction focused on one decision type.

### Stage 1: Blocking Questions

When critical information is missing, output only the questions that block product scheme or feature scope decisions:

```markdown
在推演产品方案前，需要先确认以下问题：

1. ...
```

Rules:

- Before asking Stage 1 questions, first use available codebase/project context to resolve factual uncertainties about existing project logic, APIs, fields, metric definitions, online data, key logs, user behavior, or downstream modules.
- Ask concise questions grouped by decision impact.
- Ask the product owner only for product decisions, scope choices, business intent, or facts that remain unknowable after available context checks.
- Do not output `产品方案` or `功能需求清单` in the same turn as blocking questions, unless there are only minor non-blocking assumptions.
- If there are no blocking questions, proceed to Stage 2.

### Stage 2: Product Scheme Co-Creation

After blocking questions are resolved, output only the product scheme for confirmation:

```markdown
请先确认产品方案：

- 面向用户：
- 问题场景：
- 解决方案：
- 本期做什么：
- 本期不做什么：
- 后续迭代计划：
- 关键取舍：
```

Rules:

- The product scheme must clearly answer: who the requirement serves, what user/business problem occurs in what scenario, and how the product solves it.
- This stage may be iterative. Help the product owner explore alternatives, tradeoffs, scope boundaries, and assumptions until the scheme reaches consensus.
- Do not output the feature requirement list before the product owner confirms or adjusts the product scheme.
- Do not call this output a PRD, PRD 草稿, 未确认草稿, or v0.

### Stage 3: Feature List Confirmation

After the product scheme reaches consensus, output only the feature requirement list:

```markdown
请确认功能需求清单：

| 模块 | 需求描述 | 优先级 | 备注 |
|---|---|---|---|
```

Rules:

- Include confirmed associated functional modules when the requirement extends to them.
- If commercialization affects product behavior, include the required behavior in the feature list, such as rights check, usage limit, paywall, upgrade path, package difference, pricing display, order, payment, renewal, or user-flow-changing sales/operations/customer-service wording.
- Put intentionally excluded associated modules in the product scheme's `本期不做什么`, not in the feature list.
- If new questions appear while making the feature list, ask them before writing the PRD.
- Do not generate PRD sections such as 文档信息、功能需求说明、SPEC、数据埋点、上线验收标准、发布计划、商业化、风险与依赖 before the feature list is confirmed.

### Stage 4: Frontend Design Reverse Check

After the product owner confirms both Stage 2 and Stage 3, check whether the existing frontend page misses states or interaction details that affect implementation, acceptance, launch quality, commercialization, grey release, or A/B behavior.

Output this stage outside the PRD body:

```markdown
**前端设计待补齐**

| 页面/位置 | 缺失内容 | 影响 | 建议 |
|---|---|---|---|
```

Rules:

- Output `前端设计待补齐` only when there are actual missing page states or interaction details. If none are found, say briefly that no blocking frontend design gaps were found.
- If a gap blocks implementation or launch acceptance, ask the product owner to confirm or补齐 before writing the PRD.
- If a gap is non-blocking, state it as a design follow-up and continue only after the product owner acknowledges or confirms it can be omitted.
- Do not write these gaps into the PRD body unless the product owner turns them into confirmed requirements.

### Stage 5: PRD Writing

Only after the product owner confirms both Stage 2 and Stage 3 and handles blocking frontend design gaps from Stage 4, create the formal PRD. If the user explicitly asks to skip confirmation, briefly state that this Skill requires staged confirmation before PRD正文; then continue from the earliest unconfirmed stage instead of drafting the PRD.

## Project Context Enrichment

When an authorized project-context Skill is installed and relevant, use it before finalizing product scheme or SPEC. `bi-workflow-agent` is one supported source, but the context may cover more than one project.

Default behavior: if `bi-workflow-agent` or another authorized project-context Skill is available and a question depends on existing implementation or online behavior, use it proactively. Do not ask "whether to use bi-workflow-agent" as a product confirmation question. Ask the product owner only when the result cannot be discovered from authorized context or requires a business decision.

Use project context enrichment when any of these are true:

- The requirement changes existing product logic, user flow, permission, data status, filter condition, ranking/sorting, settlement, order, membership, rights, pricing, or other business-critical behavior.
- The product scheme depends on how the current system actually works, but the user description or visible frontend page is not enough to confirm it.
- The requirement mentions online behavior, user usage, conversion, retention, complaints, abnormal data, performance, running quality, monitoring, logs, or historical incidents.
- The PRD needs online data to validate whether a problem exists, estimate affected users/orders/revenue, define grey/A/B observation signals, or judge rollout and rollback criteria.
- The feature involves an existing page/module/API whose data source, backend logic, saved conditions, cache, permission rule, or status transition is unclear.
- The requirement depends on whether an existing field, tag, enum, API parameter, route, database column, metric definition, data source, or recognition/calculation logic already exists.
- The requirement depends on online user behavior, usage volume, distribution, conversion, complaints, abnormal cases, or real data examples.
- The requirement may affect multiple projects, systems, data tables, jobs, services, or operational processes.
- The requirement adds or changes a business object, list, ranking, report, filter, metric, tag, field, status, permission, or data dimension that may have downstream or associated capabilities, such as report-center export, saved reports, subscriptions, scheduled tasks, dashboards, data permissions, search, notifications, operations tooling, or customer-service/sales usage.
- The requirement may extend to associated functional modules that need coordinated support.
- Codebase inspection and user input conflict, or the product assumption is not consistent with known online behavior.

Skip project context enrichment when all of these are true:

- The requirement is a pure copy/UI wording change with no business logic, data, permission, release, monitoring, or operational impact.
- The user already provided confirmed system facts and explicitly says no additional project context is needed.
- The task is only formatting, summarizing, or lightly reviewing an existing PRD without changing product方案 or SPEC.

- Use it to clarify current system logic, front/back-end behavior, online database facts, key logs, running quality, monitoring signals, or historical incidents.
- Use it before asking the product owner about discoverable project facts such as whether a field exists, what an API path is, how an existing metric is calculated, whether a filter/export/saved-condition path already supports a value, or how users currently behave online.
- Use it to identify associated impact surfaces and downstream changes. For example, if adding a ranking/list, check whether report-center export, saved filters, subscriptions, dashboards, permissions, data jobs, operations tooling, or related APIs also need support.
- Use it to identify whether the requirement extends to associated functional modules. For example, if changing a creator capability, check whether related modules such as creator library, report center, workbench, dashboards, export, saved conditions, or operations tools also need support.
- Use it to make product方案、功能需求清单、SPEC、埋点、上线验收标准、发布计划、风险与依赖 more consistent with real implementation and online behavior.
- Summarize findings into product decisions or PRD content. Do not paste raw logs, sensitive data, credentials, personal data, or unnecessary database rows into the PRD.
- If project context reveals contradictions with the user's initial assumption, pause and confirm with the product owner before writing the PRD.
- If project context reveals frontend design gaps, report them through the interaction output `前端设计待补齐`, not in the PRD body.
- Use only authorized capabilities exposed by the project-context Skill; do not infer or request cloud development workspace usage unless the user explicitly asks for cloud engineering development.

## PRD Rules

- Write in Chinese with a rigorous, direct, executable product-owner style.
- Treat the frontend page as the source of truth for visual design. Do not restate UI visuals already represented by the frontend page.
- Use `页面关联` only to locate where the function maps to the frontend page: page path, page position, and relation.
- Use `功能需求清单` for module-level overview only; use SPEC for detailed behavior.
- In SPEC, include `现有能力复用` only when the actual requirement or project context confirms reusable existing capability. The reused object is context-driven and may be logic, API, metric definition, permission, field, filter, export, job, report, config, module, or another existing capability.
- Do not describe reused project logic as if it were newly designed. If reuse details are unclear and materially affect implementation, confirm through codebase/project context before writing the PRD; if nothing is reused, omit `现有能力复用`.
- Do not require product owners to write technical constraints in the PRD. Only include implementation constraints when the user explicitly provides them or the codebase already makes them clear; label them as optional `实现约束（可选，研发/Agent补充）`.
- Use `上线验收标准` for requirement-level release gates. Do not duplicate every module-level SPEC acceptance case.
- Keep `商业化` lightweight. If the requirement affects commercialization, write the confirmed commercialization rules clearly; if it does not, omit the section or mark `不涉及`.
- If commercialization affects product behavior, include the behavior in `功能需求清单` and SPEC. Use `商业化` only to summarize confirmed commercialization rules; it must not replace functional requirements for rights checks, paywalls, usage limits, upgrade paths, orders, payments, renewals, or package differences.
- Mark unknowns as `待确认`; do not convert assumptions into facts.
- Do not include a `待确认问题` section in the PRD template. Critical unknowns are handled through pre-writing confirmation or interaction output.
- Do not add a post-launch summary section to the PRD template.
- Do not produce a PRD draft before the Staged PRD Gate is fully confirmed.
- Treat the PRD template as an architecture reference. Omit irrelevant sections and keep only important, necessary content for the actual requirement.
- Risks and dependencies should focus on key risks that affect launch, business monitoring, running quality, commercialization wording, rollout, rollback, or operations collaboration. Do not list internal frontend/backend development risks. If there are no key risks or dependencies, omit the section.
- When a requirement adds or changes a business object/list/ranking/report/filter/metric/tag/field/status, actively check associated impact surfaces such as export, report center, saved conditions, subscriptions, dashboards, permissions, search, notifications, tasks, operations tooling, and customer-service/sales workflows. Include confirmed associated changes in the product scheme or feature list; raise uncertain ones in the earliest relevant staged confirmation.
- For every requirement, check only whether it extends to associated functional modules. Include confirmed associated modules in `功能需求清单`; put intentionally excluded associated modules in `本期不做什么`; ask the product owner to confirm unclear associated modules before writing the PRD.
- Simple requirements may merge or omit irrelevant sections, but must not omit information that affects implementation, acceptance, release, business monitoring, running quality, or business wording.
- When project context is used, include only the product-relevant conclusions in the PRD. Keep raw diagnostics in interaction summaries, not in the PRD document.

## Frontend Design Reverse Check

Frontend design reverse checks are interaction output, not PRD content.

After product scheme and feature list are confirmed, and before drafting the PRD, if the requirement implies a frontend design state that the current page does not cover, tell the user outside the PRD:

```markdown
**前端设计待补齐**
| 页面/位置 | 缺失内容 | 影响 | 建议 |
|---|---|---|---|
```

Examples of design gaps: missing entry, missing empty/error/no-permission state, missing confirmation or feedback, missing grey/A/B hit-state handling, missing commercialization rights or price display, or missing guidance for critical operations.

If the gap blocks implementation or launch acceptance, ask the user to confirm before continuing.

## Review Mode

When reviewing an existing PRD, lead with concrete findings:

- Missing or unclear product scheme.
- Missing page association for functions.
- Functional description not SPEC-ready for engineering or AI Coding.
- Missing or unclear `现有能力复用` when actual requirement or project context shows an existing capability should be reused.
- Missing business rules, input/output, edge cases, or GIVEN/WHEN/THEN acceptance.
- Duplicated or vague acceptance standards.
- Missing data tracking, release strategy, grey/A/B observation signals, rollout criteria, or rollback criteria.
- Commercialization wording risk.
- Missing key launch/business-running risks, dependencies, or unresolved blocking questions.
- Missing use of available project context when system logic, online behavior, logs, or running data would materially affect the product scheme or requirement design.
- Asking the product owner to confirm discoverable project facts, such as existing fields, API paths, metric definitions, online usage, logs, or user behavior, before using available codebase/project context.
- Missing associated impact analysis for downstream capabilities such as report-center export, saved reports, subscriptions, dashboards, permissions, search, notifications, tasks, operations tooling, or customer-service/sales workflows.
- Missing associated functional module analysis: whether the requirement also needs coordinated support in related modules.

Then provide a focused rewrite or patch for the problematic sections.
