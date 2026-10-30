# 基础设施消费端 Harness 接入与稳定版本升级

- 状态：testing
- 消费端分支：`codex/chore-infrastructure-update`
- 接入变更提交：`89e9608`
- 旧 gitlink：`2797d8349b313b2f4dd17a8106c74ee03583475f`
- 候选及实际基础设施 commit：`fdf7e8cd14555cc1c8df0eaccd6712cbb40609ec`
- 基础设施来源：发布到稳定 `main`，同时为 `develop` 当前集成提交
- 操作者：Chaos（由 Agent 按授权执行）
- 负责人评审：Chaos 待确认

## 变更理由

让既有大工项目资产仓从 Manifest v2 发现当前已发布的共享能力，并在根 `AGENTS.md` 中安装长期消费端 Harness。固定版本通过真实 submodule gitlink 引用；不复制基础设施文件。

## Manifest 能力差异

- 升级前：Manifest schema v1，4 项能力，包括任务循环、任务记录、离线 HTML 汇报模板和 submodule 预检。
- 升级后：Manifest schema v2，10 项能力；新增小组仓模板铺设、初始化、创建并初始化、受控 submodule 更新、既有仓接入 Harness 安装和既有仓接入工作流。
- 兼容性影响：消费端 Harness 按能力 ID 和 `uses` 条件路由；README 不维护第二份能力清单。HTML 汇报模板是静态离线模板，不代表自动生成、预览或专用 HTML 检查能力已经存在。
- 实际能力清单以本仓 gitlink 固定版本中的 `manifest.yml` 为准。

## 验证证据

| 检查 | 命令或任务 | 结果 | 证据 |
| --- | --- | --- | --- |
| Harness 预览与安装 | `install_harness.py --dry-run`，再以相同计划 SHA 执行 `--apply` | pass | 计划 SHA `030c3b6cfa5d5ae627a1456063d0fa8c8bc57ba3e2df33671bc8b937bbe22db7`；仅追加 18 行 |
| 幂等复核 | 再次运行 `install_harness.py --dry-run` | pass | `agents_action: unchanged`、`would_write: false` |
| 固定版本自身回归 | `py -3 -m unittest discover -s tests -v` | pass | 85 项通过，4 项因 Windows 符号链接权限跳过 |
| 基础设施 Manifest CI | GitHub Actions run `41074246921` | pass | main 上的 Ruby Manifest、Linux 与 Windows 任务循环检查均通过 |
| 公共模板同步 | 模板仓 main gitlink 更新到同一 SHA | pass | 模板 CI run `41074341169` 成功 |
| 消费端完整预检 | `py -3 vendor/suanhai-team-external-expression-infrastructure/tools/submodule-preflight/submodule_preflight.py --root . --path vendor/suanhai-team-external-expression-infrastructure` | pass | gitlink、index、HEAD、工作区和远端 main 均一致；远端 SHA 为 `fdf7e8c` |
| Agent 运行时冒烟 | 新会话从本仓根目录读取规则、列出 Manifest 能力并对只读启动请求给出判断 | pending | 需在本消费端 Agent 客户端中实际执行 |

## 评审与回退

- 评审结论：待 Agent 运行时冒烟和负责人审阅后确认。
- 未解决问题：尚未验证目标 Agent 客户端是否自动加载根 `AGENTS.md`，也未执行真实任务或 HTML 制作。
- 回退点：`2797d8349b313b2f4dd17a8106c74ee03583475f`。
- 若试用失败：按消费端版本协议创建 `git revert`，恢复旧 gitlink，并保留本次接入记录和失败证据。

> 工程接入与 CI 通过不代表项目事实已核验、内容已获专业确认或对外发布已经授权。
