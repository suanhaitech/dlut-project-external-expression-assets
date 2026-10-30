# 评审与确认记录

`reviews/` 保存作品和任务的评审意见、修订记录、基础设施版本升级/回退记录、待解决问题、责任收口和真人确认。

工程检查、内容评审、专业判断和对外发布授权应分开记录。评审文件存在不等于所有意见已经解决，也不等于作品已经获得发布许可；记录应注明状态、责任人和适用版本。

## 基础设施版本升级记录模板

需要更新 `vendor/suanhai-team-external-expression-infrastructure` 时，复制以下字段到独立的升级任务记录中。父仓库 gitlink 是实际使用版本的唯一事实来源，不要在其他配置文件中维护第二份版本锁。

```markdown
# 基础设施版本升级：<简短目的>

- 状态：draft / testing / accepted / rejected / reverted
- 消费端父仓提交：`<parent-commit>`
- 旧 gitlink：`<old-infrastructure-commit>`
- 候选新 commit：`<candidate-infrastructure-commit>`
- 实际检出 commit：`<checked-out-infrastructure-commit>`
- 预检时间：`<ISO-8601>`
- 操作者：`<真人姓名或团队身份>`

## 变更理由

<需要获得的能力、修复的问题和为什么现在升级>

## Manifest 能力差异

- 升级前：`<capabilities 快照或链接>`
- 升级后：`<capabilities 快照或链接>`
- 兼容性影响：<无 / 说明>

## 验证证据

| 检查 | 命令或任务 | 结果 | 证据 |
| --- | --- | --- | --- |
| submodule 预检 | `python vendor/.../tools/submodule-preflight/submodule_preflight.py ...` | pass/fail | `<输出或文件>` |
| Manifest | `ruby scripts/validate_manifest.rb` | pass/fail | `<基础设施提交或 CI>` |
| 消费端冒烟 | `<命令或任务编号>` | pass/fail | `<记录路径>` |
| 真实任务试用 | `<任务编号>` | pass/fail/未执行 | `<记录路径>` |

## 评审与回退

- 评审结论：<接受 / 拒绝 / 需要补充>
- 未解决问题：<无 / 列出>
- 回退点：`<old-infrastructure-commit>`
- 若回退：父仓回退提交、失败证据和恢复后的预检结果

> 这份记录不替代专业事实评审或发布授权。升级失败时优先用父仓 `git revert` 保留审计链，不使用 `reset --hard`、`clean` 或强制推送覆盖未知修改。
```

当前已有工程验证记录：

- [基础设施消费端 Harness 接入与稳定版本升级（2026-10-30）](infrastructure-adoption-fdf7e8c-2026-10-30.md)：记录既有仓库安装根 Harness、固定基础设施稳定版本和待完成的 Agent 运行时冒烟。
- [Agent 只读启动冒烟测试（2026-10-28）](bootstrap-smoke-2026-10-28.md)：验证启动协议与能力发现，不替代作品评审或发布授权。
- [任务循环接入与恢复验证（2026-10-28）](task-loop-validation-2026-10-28.md)：验证任务状态、反馈与续作；合成测试不构成真实业务或发布确认。
- [HTML 模板套用试点验证（2026-10-28）](template-pilot-validation-2026-10-28.md)：验证固定 submodule 中的离线模板可以被消费端发现、套用和记录。
