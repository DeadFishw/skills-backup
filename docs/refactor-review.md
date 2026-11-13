# 四 Skill 重构记录 — 2026-11-13

## 范围与恢复基线

对象是本机实际安装的七个用户级 Skill。修改前逐文件比较，27 个文件与 GitHub 固定提交 `4f608910f4041b82641fa488f440816bea6da173` 完全一致。保留该提交和原 `backup-manifest.json`，新内容在本地 `refactor/four-skill-workflow` 分支工作。

本机先建立完整文件快照和私有配置备份；旧目录及被替换的参考资料移到 Skill 发现目录外。没有修改内置 Skill、其他 Skill 或项目源码。最终本机安装检查见下文。此报告及本地 commit 不表示已获 GitHub 推送授权。

## 职责与按需加载

| 主负责人 | 触发与完成边界 |
| --- | --- |
| Think | 复杂规划、架构和重要技术决策，或明确的计划／实施证据审查。默认只读；仅授权后写持久记录。返回所请求的计划或审查即停止 |
| Work 普通模式 | 明确开发请求。理解、实现、验证、检查 diff、报告完成；不自动添加 Planner Review |
| Work 严格模式 | 本次执行相关已批准合同、用户明确要求严格模式、或项目规则要求。验证后提交 Developer Report，交给要求的审查环节 |
| Coordinator | 用户明确请求完整周期或项目明确要求。风险决定独立 Plan Review，保留独立 Final Review，再执行获授权的收尾 |
| No Negative Echo | 用户已经否决方案、命名或措辞后的特殊最终交付。只处理无用的会话残留，保留审计、兼容性及其他必要事实 |

三个开发 Skill 安装在同一父目录。共享状态和记录规范只有一个权威文件：`think-like-i11usion/references/workflow-protocol.md`。普通 Work 不加载它。复杂规划、审查、协调与收尾的细节按阶段读取。

## 必要功能迁移与兼容性

| 原功能 | 新权威来源 |
| --- | --- |
| 项目事实重建、关键假设、方案比较、完整切片、验收矩阵 | Think + planning-contract.md |
| 状态恢复、批准来源、双计划 lane、历史兼容、报告与 Verdict | workflow-protocol.md |
| 简单性、精确修改、接口保留、既有依赖、错误边界、由小到大的验证 | Work |
| 真实证据审查、逐条验收、多 lane 分别评估、脏改动依赖、缺失证据 | Think + planner-review.md |
| 风险决定独立计划审查、角色隔离、实施者交接、审查不可用 | Coordinator + lifecycle.md |
| 幂等归档、历史菜单与锚点、只重置已审 lane、保护无关 hunks、分项授权提交发布 | Coordinator + closeout.md |

退役的 `prepare-development-step`、`planner-doc-review`、`karpathy-guidelines` 不再拥有独立流程。四个保留 Skill 的发现说明和协议提供旧名映射。原有 `next_step.md`、`next_step2.md`、`next_step_2.md` 路径、历史状态拼写及项目模型要求保留，不批量改写项目文件。

新记录统一使用：`PROPOSED → READY → IMPLEMENTING → PENDING_REVIEW → ACCEPTED → CLOSED`；失败和等待分支是 `CHANGES_REQUIRED`、`BLOCKED`。状态、检查结果、验收结果和审查 Verdict 分别定义，历史记录按语义解释。

项目副本可能继续存在。因此除移出全局活动目录，还在本机配置末尾添加以下按名称停用项，保留其他配置：

```toml
[[skills.config]]
name = "prepare-development-step"
enabled = false

[[skills.config]]
name = "planner-doc-review"
enabled = false

[[skills.config]]
name = "karpathy-guidelines"
enabled = false
```

按名停用覆盖同名项目副本；用真实 Codex `skills/list(forceReload=true)` 检验，而非只看文件目录。原项目的独立审查、模型约束和明确的归档提交要求仍然有效。本轮用户限定计划或审查时，应停在该边界。

## Context 成本

Token 用同一方法估计：每份文本 Unicode 字符数除以 4 向上取整。它适合这些主要为英文的规则的相对比较，不是精确模型计费。仅统计本次七个 Skill 的范围；报告、清单和私有恢复快照不参与 Skill 自动加载。

| 指标 | 修改前 | 修改后 |
| --- | ---: | ---: |
| 活动 Skill | 7 | 4 |
| 活动 Skill 内全部文件 | 27 | 20 |
| SKILL.md 估算 Token 合计 | 19,428 | 2,907 |
| 名称与 description 发现成本 | 898 | 268 |
| Reference 文件 | 8 | 6 |
| Reference 估算 Token 合计 | 12,433 | 5,707 |

| Skill | 原文件数 → 新文件数 | 原入口 Token → 新入口 Token |
| --- | ---: | ---: |
| think-like-i11usion | 4 → 5 | 1,382 → 502 |
| work-like-i11usion | 4 → 2 | 1,811 → 793 |
| plan-review-implement-review | 5 → 4 | 2,605 → 622 |
| no-negative-echo | 8 → 9 | 965 → 990 |
| prepare-development-step | 2 → 0 活动 | 4,804 → 0 活动 |
| planner-doc-review | 1 → 0 活动 | 7,110 → 0 活动 |
| karpathy-guidelines | 3 → 0 活动 | 751 → 0 活动 |

入口估算减少约 85%，发现成本约 70%。Think 增加共享协议，No Negative Echo 补充 LICENSE；文件数不是单独的优化目标。

重复统计采用人工的“额外完整职责定义”口径，不是词句相似度：

| 核心规则组 | 原独立定义所在 Skill | 新权威来源 |
| --- | --- | --- |
| 规划步骤 | Think、Prepare、Coordinator | Think |
| 实施原则 | Work、Karpathy | Work |
| 实施审查 | Think、Planner Doc、Coordinator | Think |
| 生命周期调度 | Prepare、Coordinator | Coordinator |
| 状态与记录 schema | Think、Work、Prepare、Planner Doc、Coordinator | 共享协议 |
| 风险计划审查 | Prepare、Coordinator | lifecycle.md |
| 归档、重置和提交收尾 | Prepare、Planner Doc、Coordinator | closeout.md |
| Writer 分配与交接 | Prepare、Coordinator | lifecycle.md |

以上八组共 22 个定义归并为 8 个权威定义，额外定义从 14 个降为 0。入口保留必要的路由和权限提醒，不把它们计为重复的完整规则。此统计没有声称所有自然语言提醒都只出现一次。

自动触发覆盖从六个有重叠的开发 Skill 收敛到三个不同阶段角色：普通实现由 Work；复杂规划或明确审查由 Think；完整周期才由 Coordinator。No Negative Echo 始终是独立的特殊交付能力。

## 已执行的场景测试

使用独立 Agent 新上下文，仅提供候选库和原始任务，不提供预期 Skill 或正确结果。每个写入场景有独立 Git 仓库，不能改真实项目或提交发布。

按用户目标判断，表中列出的角色应触发，其他角色不应接管任务。普通修复不应追加审查或状态更新；规划、只审查和文案请求应保持其只读边界；批准合同应等待审查；完整周期应保留真实独立终审。这些是测试后比对的判定标准，未预先提供给测试 Agent。

| 场景 | 实际选择与 Reference 数 | 实际结果与停止点 |
| --- | --- | --- |
| 简单 Python Bug，另有无关批准计划与用户 dirty 文件 | Work 普通；0 | 先复现整数除法错误，修复后 2 测试通过；保留空输入异常、无关计划和用户改动；直接完成 |
| 多租户 Agent 架构规划，设计文档与源码矛盾 | Think；1 | 按证据识别隔离缺失，比较三种方案、列假设和可验证验收；只读停止 |
| 执行批准的 parser 合同 | Work 严格；1 | 新用例先失败，修复后 5 测试通过；写真实 Developer Report，停在 PENDING_REVIEW |
| 显式完整 Plan–Implement–Review | Coordinator + Think + Work；合计 4 | 低风险计划审查记录 SKIPPED；实际实现、原测试、单数及 7 个保留行为检查通过；另一个只读 Agent 真实终审 APPROVED；仅获授权本地记录收尾，CLOSED，无提交发布 |
| 多次否决命名后的最终文案 | No Negative Echo；0 | 输出确定名称、两句事实简介与文件名；无历史残留，无写文件或发布 |
| 项目通常归档提交，本轮只审查 | Think；2 | 仅说明证据审查，不更新状态、归档、提交；没有实际补丁就不虚构通过 |
| 跨会话 Writer 替换，缺少独立 Reviewer | Coordinator + Work；2 | 允许核验交接后继续获授权修复；最终审查诚实报告 REVIEW_UNAVAILABLE / BLOCKED，不自审冒充独立批准 |

前三个、完整周期和文案场景分别由新的 Agent 执行；最后两个只读边界请求由同一个新的测试 Agent 分别评估。完整周期的终审由再次新建的 Reviewer 执行，未参与规划和实现。

旧版普通 Work 明确要求实施和报告两份 Reference，新版简单场景实际为 0。复杂规划两版通常均需 1；严格实现由原来的 2 份降为实测 1 份。完整周期不是强行最少文件：新版低风险测试按阶段读了 4 份，复杂规划还需 planning-contract.md；旧版协调本身有 3 份、组合角色时另加其 Reference。文案两版均可不加载 Reference。

## 结构、安装、恢复和来源验证

- 四个 Skill 通过随 Codex 提供的 `skill-creator/scripts/quick_validate.py`。
- 附加检查通过：frontmatter、名称及 description、UI 元数据、图标路径、所有本地 Markdown 引用、Python AST、MIT 版权与完整许可。
- 扫描器实际运行七例：接受文本、内容残留、文件名残留、Unicode 全角归一化、UTF-16、零宽字符、空词表错误；返回结果及退出码符合预期，不回显被否决词。
- 针对凭据、私钥、私有网络 URL、绝对用户路径的模式检查通过，并人工审读保留内容。原私有配置只备份到本机，未加入公开仓库。
- 恢复脚本在临时目录演练通过：27 个原始文件恢复，20 个候选文件另存，无关配置保留；只读预检不改文件。
- `no-negative-echo` 来源为 LB623 上游；补回 Copyright (c) 2026 LB623 的完整 MIT LICENSE。原 provenance 的哈希明确标记为导入来源哈希，本地变化单独记载，新清单记录当前哈希。
- 本机安装回读通过：四个活动目录逐字节等于候选，三个停用目录逐字节等于原快照；171 个无关 Skill 文件和 11 个被检查的项目说明／Skill 文件哈希未变。
- Codex 0.164.0-alpha.11.1 的新 app-server 在通用工作区、两个项目及一个 worktree 共四个上下文强制重新扫描：本次范围仅四个保留项启用，三个旧名启用数为 0；发现的项目副本均为 enabled=false。通用工作区全部启用 Skill 数为 45 → 42，没有新增解析错误。
- 公开候选和文档共 20 个文本文件通过定向敏感信息扫描；24 个本地 Markdown 链接有效。20 个活动文件没有逐字节重复文件。原始 27 个文件同时核对 Git 对象、manifest 和本地快照，全部一致。
- 额外新 Agent 旧名路由测试通过：规划和只审查两个请求均从发现说明正确选到 Think，保留 next_step_2.md、历史格式和项目模型约束，不寻找或重启旧 Skill，不归档提交。
- 独立内容审查检查了原七个与候选四个，首次结论 APPROVED_WITH_NOTES，无阻断问题。已采纳唯一措辞建议：APPROVED 明确要求所有必需验收项 PASS 且无阻断发现；结构检查与安装哈希已复验。相同审查者复核修正和证据后最终 APPROVED；报告引用成本同步修正为 5,707。

## 限制与后续使用

架构场景没有成功运行运行时探针；判断由已读取源码和明确未知项支撑，没有把探针计为通过。两个边界场景只验证流程决策，不声称实际交接或故障恢复已经执行。

测试覆盖了真实执行、独立终审和原生发现元数据，但不是每个模型、所有真实项目或多轮自动选择的统计评测。当前 Codex 会话已装入的旧 Skill 说明无法在原上下文中移除，重启 Codex 并新开任务后使用新目录与停用配置。

发现一个不在本次范围的既有 Skill `write-novel-chapter` 缺少 YAML frontmatter；此次未修复它。项目今后如果加入覆盖这些停用项的新配置，需重新检查实际发现结果。

原 GitHub 主分支保留备份；本次改动只在用户审阅 Diff 并确认后推送。恢复时优先使用本机快照和演练过的恢复脚本，或在独立目录检出固定的原始 Git 提交。不要直接用旧快照覆盖后来产生的工作。
