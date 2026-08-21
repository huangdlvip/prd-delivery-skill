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

将 `<OWNER>/<REPO>` 替换为实际 GitHub 仓库，例如 `yourname/prd-delivery-skill`。

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo <OWNER>/<REPO> \
  --path skills/prd-delivery
```

安装后，在新的 Codex 对话中即可使用：

```text
使用 prd-delivery 帮我写一个 xxx 需求的 PRD
```

## 更新

当前安装器在目标 Skill 已存在时会中止。团队成员更新时，先删除本地旧版本，再重新安装：

```bash
rm -rf ~/.codex/skills/prd-delivery
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo <OWNER>/<REPO> \
  --path skills/prd-delivery
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

