# Relationship Map Maintenance

English version: [README.md](./README.md)

`relationship-map-maintenance` 是一个面向项目的 skill，用来给复杂代码改动维护一层轻量的关系图与影响面文档。

它适合这类仓库：一个修复或功能往往会跨越代码、配置、脚本、运行时链路和测试，而且项目里经常出现“只改了一处，遗漏了另一处”的问题。

这个 skill 不替代代码阅读、测试和 review。它的作用是补一层成本可控的书面结果，让 agent 在改动前更容易定位影响范围，在改动后更容易同步更新相关关系。

## 作用

- 为 `docs/<project-scope>/relationship-map/` 提供一套项目级文档结构
- 为项目根 `AGENTS.md` 提供一段最小常驻规则，保证压缩或重入后仍有基础路由能力
- 用 `critical-chains/` 和 `impact-shards/` 表达高价值的改动链路
- 用 `generated/00_manifest.md` 管理生成型证据，避免默认扫描整目录
- 用保守的维护规则处理冲突、生命周期、审计和自动化

## 设计原则

- 默认路径尽量短
- 优先路由，再决定是否展开阅读
- 优先复用已有文档结果，避免反复重新分析
- 维护成本要低于它试图避免的遗漏成本
- 结构性或破坏性动作必须显式处理

## 默认工作方式

默认主路径分为三段：

- `use`：改动前先做路由和影响面判断
- `update`：改动后只更新真正被触及的关系项
- `maintain`：仅在需要时做周期性维护

维护模式分为三档：

- `skip`：关系中立或局部机械改动，不读取 relationship-map 文档
- `light`：只读 `00_index.md` 和最小相关 shard 的摘要
- `full`：仅在高风险、多表面、结构性改动或 `light` 不足时展开

## 目录结构

```text
relationship-map-maintenance/
  SKILL.md
  README.md
  README.zh-CN.md
  LICENSE
  agents/
    openai.yaml
  assets/
    AGENTS.relationship-map-snippet.template.md
    00_index.template.md
    01_usage_and_policy.template.md
    02_audit_log.template.md
    critical-chain.template.md
    impact-shard.template.md
    generated-manifest.template.md
    maintenance-report.template.md
    automation-prompt.template.md
  references/
    audit-and-automation.md
    automation-workflow.md
    conflict-lifecycle-and-deletion.md
```

## 安装

把整个 skill 目录复制到 Codex 的 skills 目录下即可。

如果按项目安装，就放到仓库本地的 skills 目录。
如果按用户级安装，就放到用户自己的 Codex skills 目录。

## 初始化

初始化分两层：

1. 在 `docs/<project-scope>/relationship-map/` 下创建关系图文档层
2. 把最小的 relationship-map 常驻规则接入项目本地 `AGENTS.md`

`AGENTS.md` 的接入方式必须是增量式：

- 如果项目已经有 `AGENTS.md`，只追加 relationship-map 片段
- 不改写、不重组无关的 `AGENTS.md` 内容
- 只有项目没有 `AGENTS.md` 时才创建

对应片段模板在 `assets/AGENTS.relationship-map-snippet.template.md`。

## 适用场景

适合在这些场景中使用：

- 一个 bug 修复会跨多个文件或多个表面
- 改动触及共享契约、入口点或核心配置格式
- 项目里经常因为链路关系不清晰而残留 bug
- 你希望把影响关系沉淀成可复用结果，供后续改动和审查继续使用

但它不能单独替代实现和审查。
代码阅读、测试、运行验证和直接搜索仍然是必要的。

## 维护与自动化

这个 skill 的维护策略是保守的：

- 可以刷新生成型证据
- 可以标记过期或冲突的 shard
- 只有在出现实质发现，或者定时任务明确要求时，才建议写维护报告
- 不应静默执行结构性 shard 变更
- 物理删除必须得到用户明确批准
