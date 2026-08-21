# prd-delivery Skill

中文交付型 PRD 创建、评审、需求拆解和研发友好化 Skill。

适用于产品、研发在 Git 代码库中协同，产品直接基于前端页面替代原型，研发基于前端页面和 PRD 完成业务开发、自测和上线的快速迭代工作流。

## 能力范围

- 从 0 到 1 写 PRD
- PRD 评审
- 需求拆解
- 产品方案推演
- 研发友好化 / AI Coding 友好化
- 上线与验证
- 前端设计反向校验
- 项目上下文增强

## 工作流

1. 先读取需求、代码库、页面、分支、PR 或已有文档。
2. 如已授权项目上下文能力，先查代码库、接口、字段、指标口径、线上只读数据库、关键日志或用户行为数据。
3. 只向产品确认查不到、且会影响方案或范围的阻塞问题。
4. 与产品共创并确认产品方案：面向用户、问题场景、解决方案、本期做什么、不做什么、后续迭代、关键取舍。
5. 产品方案确认后，再确认功能需求清单。
6. 写 PRD 前反向检查前端页面缺失的异常态、空态、权限态、失败提示、二次确认等。
7. 最后生成正式 PRD，使用模板作为架构参考，不涉及的部分不写。

## 安装

在 Codex 里直接对 Agent 说：

```text
帮我安装 PRD Skill https://github.com/huangdlvip/prd-delivery-skill/tree/main/skills/prd-delivery
```

Agent 会使用内置 `skill-installer` 安装这个 Skill。安装完成后，开启新的 Codex 对话即可使用：

```text
使用 prd-delivery 帮我写一个 xxx 需求的 PRD
```

也可以手动执行：

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/huangdlvip/prd-delivery-skill/tree/main/skills/prd-delivery
```

## 更新

在 Codex 里直接对 Agent 说：

```text
帮我更新 PRD Skill https://github.com/huangdlvip/prd-delivery-skill/tree/main/skills/prd-delivery
```

如果 Agent 提示本地已存在旧版本，可以让 Agent 删除旧版后重新安装。手动更新方式：

```bash
rm -rf ~/.codex/skills/prd-delivery
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/huangdlvip/prd-delivery-skill/tree/main/skills/prd-delivery
```

## 仓库结构

```text
skills/prd-delivery/
├── SKILL.md
├── agents/openai.yaml
├── assets/prd-template.md
└── references/
    ├── acceptance-standards.md
    ├── release-plan.md
    └── spec-writing.md
```
