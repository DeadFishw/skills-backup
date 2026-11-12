# Skills backup

2026-11-12 备份的 7 个全局 Codex skill，来源为本机用户级 skills 目录。

| Skill | 文件数 |
| --- | ---: |
| [think-like-i11usion](skills/think-like-i11usion/SKILL.md) | 4 |
| [work-like-i11usion](skills/work-like-i11usion/SKILL.md) | 4 |
| [plan-review-implement-review](skills/plan-review-implement-review/SKILL.md) | 5 |
| [planner-doc-review](skills/planner-doc-review/SKILL.md) | 1 |
| [prepare-development-step](skills/prepare-development-step/SKILL.md) | 2 |
| [karpathy-guidelines](skills/karpathy-guidelines/SKILL.md) | 3 |
| [no-negative-echo](skills/no-negative-echo/SKILL.md) | 8 |

共 27 个原始文件，完整保留说明、参考资料、脚本、配置和图片资源。

## 校验

`backup-manifest.json` 记录每个原始文件的路径、字节数、SHA-256 和 Git blob SHA。`skills/` 内的文件按原始字节保存，`.gitattributes` 禁用该目录的换行转换。

## 恢复

下载或克隆本仓库，将 `skills/` 下需要恢复的整个 skill 文件夹复制到本机 Codex 用户级 skills 目录，例如 Windows 的 `%USERPROFILE%\.codex\skills\`。保留各 skill 内的相对目录结构；覆盖已有版本前先比较内容并保存现有版本。

这是本次手动备份的快照。以后修改本地 skill 后，需要再次提交并上传更新。
