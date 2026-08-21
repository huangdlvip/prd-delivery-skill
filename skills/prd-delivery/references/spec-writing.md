# SPEC 功能描述

Use SPEC 功能描述 to make PRD sections executable for engineers and AI Coding agents. Keep it precise, but adjust fields to the actual requirement.

## Required Structure

```markdown
### {功能模块}

#### 功能目标
说明该功能要解决什么问题，达成什么结果。

#### 页面关联
- 页面路径：
- 页面位置：
- 关联说明：

#### 现有能力复用
说明本需求复用的现有逻辑、接口、指标口径、配置或模块；没有则不写本节。

#### 输入 / 输出
- 输入：
- 输出：
- 成功：
- 失败：

#### 业务规则
- ...

#### 边界与异常
- ...

#### 验收标准
- GIVEN ... WHEN ... THEN ...

```

## Writing Rules

- Page association only identifies where the function maps to the frontend page. Do not describe visual details already represented by the frontend page.
- Use real paths, routes, component names, or visible page regions when available. If unknown, write `待确认`.
- Use `现有能力复用` only when actual requirement context or project context confirms reusable existing capability. The reused object is context-driven and may be logic, API, metric definition, permission, field, filter, export, job, report, config, module, or another existing capability; do not force fixed categories.
- Do not include `现有能力复用` when nothing is reused or when reuse is only a guess. Do not rewrite existing logic as new business rules. If the requirement only changes part of an existing capability, separate reused behavior from newly added or adjusted behavior only when needed.
- Input/output may describe API requests/responses, user input/system feedback, data imports/exports, configuration changes, or scheduled job behavior.
- Business rules must avoid vague verbs such as `支持`, `优化`, `完善`, `处理` without concrete conditions and results.
- Edge cases must cover common failure modes: empty data, no permission, duplicate operation, invalid input, interface failure, timeout, stale data, limits, and rollback-sensitive states.
- Acceptance standards should use GIVEN / WHEN / THEN. Prefer observable results, stored data, returned codes, emitted events, or visible user feedback.
- Do not require product owners to write technical constraints in the PRD. Technical constraints are implementation-stage content unless the user explicitly provides them or the existing codebase already makes them clear.
- If implementation constraints are known and materially affect AI Coding, add them as a short optional note outside the required SPEC structure, labeled `实现约束（可选，研发/Agent补充）`.

## Example

```markdown
### 头像上传

#### 功能目标
支持用户上传头像图片，用于个人资料展示。

#### 页面关联
- 页面路径：`src/pages/profile/index.tsx`
- 页面位置：个人资料页头像区域
- 关联说明：点击头像编辑按钮后触发头像上传流程。

#### 现有能力复用
- 复用现有用户资料编辑权限校验。
- 头像上传成功后沿用现有资料页刷新和头像展示逻辑。

#### 输入 / 输出
- 请求：`multipart/form-data`，字段 `file`（必填）
- 成功：200，返回 `{ "url": "https://cdn.xxx.com/avatar/xxx.jpg" }`
- 失败：返回统一 JSON 结构 `{ "code": 413, "message": "..." }`

#### 业务规则
- 仅支持 jpg / png / webp，最大 5MB。
- 存储到 OSS，路径 `/avatar/{user_id}/{yyyy-mm}/{uuid}.{ext}`。
- 生成 3 种尺寸缩略图：128 / 256 / 512。

#### 边界与异常
- 文件超 5MB -> 413 `文件不能超过 5MB`。
- 格式不支持 -> 415 `仅支持 jpg/png/webp`。
- 服务端校验真实文件类型，不信任 Content-Type；伪装扩展名 -> 415。
- 文件名包含非法字符 -> 自动替换为 uuid。
- 单用户每分钟最多上传 10 次，超限 -> 429。

#### 验收标准
- GIVEN 上传合法 jpg WHEN 提交 THEN 返回 200 且 OSS 存在文件。
- GIVEN 上传 6MB 文件 WHEN 提交 THEN 返回 413 且不落库。
- GIVEN 伪装成 jpg 的 exe WHEN 提交 THEN 返回 415。

#### 实现约束（可选，研发/Agent补充）
- 后端 Spring Boot 3.x，OSS SDK 用腾讯云 COS v5。
- 不新增非必要依赖；错误码遵循项目 ErrorCode 规范。
```
