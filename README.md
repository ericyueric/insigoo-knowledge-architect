# 知识库架构师 · 开源通用 Agent 角色

> 基于 [insigoo-sag-architect](https://github.com/ericyueric/insigoo-sag-architect)（SAG 知识库架构师方法论）的通用 agent 角色配置。组织建好知识库后，用本角色让 agent 真正「活」起来——建库、编译、诊断三件事的编排者。

## 定位

开源通用的「知识基础设施」agent 角色。负责 **建库（SAG）× 编译（管理-披露标准 + GDT-Core）× 诊断（SIA）** 的编排，不参与业务执行。默认内置公益/社会组织最佳实践，可适配任意行业组织。

本角色是 insigoo-os 标准 agent 角色之一，但**可独立使用**——只需主技能 `insigoo-sag-architect` 已安装。

## 主技能与依赖

| 技能 | 作用 | 必装 |
|------|------|------|
| `insigoo-sag-architect`@2.0.0 | 本角色主技能：建库 + 编译 + 诊断编排 | ✅ 必装 |
| `insigoo-knowledge-base`@2.0.0 | 组织知识库建设标准（LLM Wiki 三层索引 + GDT v1.1，通用版） | 推荐 |
| `insigoo-sag` | SAG 语义检索引擎 + LLM Wiki（能力一技术底座） | 可选 |
| `insigoo-sia`@2.0.0 | L1 逻辑体检（开源版仅含 L1；L2/L3 见其开源仓库） | 可选 |

## 接入 dsh（harness）

本目录是一个 dsh preset（含 `agent.cordis.yml` + `preset.yml`）。放到 dsh 的 preset root 即被自动发现：

```bash
cp -r knowledge-architect ~/.dsh/.agent-presets/
dsh --profile web     # 选择器出现「知识库架构师」
```

`agent.cordis.yml` / `preset.yml` 由 `../generate.mjs` 从四件套 `.md`（agent.md / soul.md / memory.md / collab.md）单向编译生成。改角色请改 `.md` 后重跑 `node ../generate.mjs`，勿手改生成产物。

## 可配置项

- **组织类型**：角色默认内置公益/社会组织最佳实践。适配其他行业时，在任务上下文声明组织类型即可，无需改角色文件。
- **总编排 agent 名**：本角色作为 sub-agent 时由 main agent 委派；main agent 名在你的编排层配置，不写死在角色内。
- **底层技能版本**：`insigoo-sag-architect` / `insigoo-sia` 版本号在 `agent.md` 的 skill 加载约定中声明，升级时同步修改即可。

## 分层原则（铁律）

人格层（.md）↔ 能力层（SKILL.md）↔ 知识层（SAG），三层互不重复。.md 只写约束兜底 + 路由 + 人格，方法细节引用 skill，不固化可调度口径。

## 与其他角色的关系

在 insigoo-os 全集中，本角色与「数据分析师（GDT-DB）/ SIA 诊断 / 课程开发 / 总编排」协作。独立使用时，仅需本目录 + `insigoo-sag-architect` 主技能；其余角色按需接入。

## 相关开源仓库

- [insigoo-agents](https://github.com/ericyueric/insigoo-agents) — insigoo OS 标准 agent 角色配置（开源 MIT）：总编排 / 数据分析师 / SIA 诊断 / 课程开发 四件套 + dsh preset 生成器。
