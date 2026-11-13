# Skills backup

四个互补的用户级 Codex Skill。开发流程按复杂度加载，特殊文案收尾单独使用。

| Skill | 职责与触发 |
| --- | --- |
| [think-like-i11usion](skills/think-like-i11usion/SKILL.md) | 复杂规划、架构决策和明确的计划／证据审查；默认只读 |
| [work-like-i11usion](skills/work-like-i11usion/SKILL.md) | 明确开发请求默认直接实现、验证和报告；执行批准合同或项目要求时进入严格模式 |
| [plan-review-implement-review](skills/plan-review-implement-review/SKILL.md) | 用户明确请求或项目要求的完整生命周期；保留独立最终审查 |
| [no-negative-echo](skills/no-negative-echo/SKILL.md) | 用户否决过命名、措辞或方案后的最终交付检查 |

三个开发 Skill 共用 Think 中的 [workflow-protocol.md](skills/think-like-i11usion/references/workflow-protocol.md)。安装时一并复制它们，保留兄弟目录关系；`no-negative-echo` 可以单独安装。优先使用本机实际的用户级 Skill 目录，不同时安装多份同名技能。

`prepare-development-step`、`planner-doc-review`、`karpathy-guidelines` 已迁移并停用。原文件保留在本机发现目录之外的恢复快照，以及下面固定的 Git 历史版本中。项目仍引用旧名称时，共享协议提供职责映射并保留项目的实际要求。迁移时还应按名称禁用旧 Skill，防止项目副本继续自动加载；具体配置和验证见 [重构报告](docs/refactor-review.md)。

## 原始备份与校验

2026-11-12 的 **7 个 Skill、27 个文件**固定在提交 [`4f608910f4041b82641fa488f440816bea6da173`](https://github.com/DeadFishw/skills-backup/tree/4f608910f4041b82641fa488f440816bea6da173)。该原始提交不变。

- [backup-manifest.json](backup-manifest.json) 仍只描述原始快照，保持原字节。
- [current-manifest.json](current-manifest.json) 描述本次四个 Skill 的文件、大小和 SHA-256。
- `.gitattributes` 禁用 `skills/` 换行转换，便于逐字节核验。

## 恢复

恢复原始版本时，在另一个目录检出上述固定提交，核对原始 manifest，再复制整个所需 Skill 目录。覆盖前先将当前版本移到发现目录外保存。恢复已停用的三个 Skill 时，还需移除本次迁移添加的三个 `skills.config` 按名称停用项，再重启 Codex。

本机另有完整快照、配置备份和已演练的恢复脚本，位置及命令见本地交付报告。私有配置备份不属于此公开仓库。仓库更新是手动操作，修改本机文件不会自动同步 GitHub。

## 来源与许可

`no-negative-echo` 来自 [LB623/no-negative-echo](https://github.com/LB623/no-negative-echo)，保留原作者版权、[MIT LICENSE](skills/no-negative-echo/LICENSE) 和来源记录。其余 Skill 的既有来源未统一声明授权；此仓库不额外为全部内容授予 MIT 许可。
