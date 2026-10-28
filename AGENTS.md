# Agent 协作约定

本仓库是大工项目小组的对外表达资产仓库。Agent 的工作目录是本仓库根目录，项目事实、任务上下文、来源、作品和评审记录都以本仓库为主位。

## 开始任务前

1. 读取根 `README.md` 和本文件；
2. 读取 `vendor/suanhai-team-external-expression-infrastructure/manifest.yml`；
3. 读取 `vendor/suanhai-team-external-expression-infrastructure/docs/consumer-repository-bootstrap.md`；
4. 读取 `vendor/suanhai-team-external-expression-infrastructure/docs/consumer-repository-harness-v0.1.md`；
5. 读取 `vendor/suanhai-team-external-expression-infrastructure/docs/submodule-consumer-versioning.md`，了解固定版本预检、升级和回退协议；
6. 读取 `context/README.md`，按其阅读顺序理解项目结构化理解、项目概览、当前状态、工作主线、来源登记和对外表达边界；
7. 用户给出任务号时，先用 Manifest 中的任务记录工具 `show` 读取 `tasks/<任务号>/task.json`，核对当前状态、历史、产出和下一步；`task.md` 是生成阅读视图，不单独手改；历史任务则按其既有格式读取；
8. 只按 Manifest 中显式列出的能力发现和使用基础设施，并判断输出应进入 `works/`、`series/`、`courses/` 或 `books/` 中的哪个位置。

首次工作前，先报告当前项目、任务是否存在、受众与目的、允许使用的来源、计划输出路径、共享能力、缺失信息和需要真人确认的事项。事实摘要与表达边界以本仓库为准，共享协议不能覆盖更严格的本地规则。

未指定任务或当前只有 `tasks/README.md` 时，只读启动不得自行创建任务或作品；应明确报告缺少任务，并停在作品生成前。用户已提出实际制作需求并授权写入时，读取 Manifest 中 `expression.task-loop` 的入口，先通过 `expression.task-record` 创建草案和任务号，再澄清关键目标；不能把路线图中的计划当作已登记任务。

任务循环采用“用户澄清/评审”和“Agent制作/检查”两层：目标对齐后，在授权范围内连续制作检查；小范围反馈直接修订，目标范围变化回到澄清。用户确认本轮后记录实际产出版本、限制、任务号和续作方法；专业验收与发布授权分别判断。

暂停时保留状态和下一步；换会话先只读恢复，获得续作请求后再 resume 或 reopen，不重建同一任务。旧确认版本使用独立路径保存，不覆盖。已有任务写入使用工具的 `--expect-version`，冲突时重新读取并保留其他操作者的变更。

submodule 或上述协议文件缺失时，报告未完成初始化或版本不匹配，不虚构其内容；先由用户或已获授权的操作完成 submodule 初始化，再继续协议测试。

## 基础设施版本启动预检

每次进入本仓库开始工作时，先执行一次只恢复父仓库锁定版本的初始化：

```powershell
git submodule update --init --recursive
```

该命令不会追踪远程分支，也不会把 submodule 更新到远程最新版本。随后使用当前 Manifest 声明的 `consumer.submodule-preflight` 入口进行只读预检，至少确认父仓库 gitlink、submodule 实际 `HEAD`、工作区状态和远程稳定分支快照。预检输出中的实际 commit 应写入本次任务或评审记录。

预检结果只用于判断“当前固定版本是否可复现”和“是否有可供人工评估的更新提示”：

- `locked`：父仓库 gitlink 与 submodule `HEAD` 一致，工作区干净；
- `dirty`、`missing` 或 `unknown`：先报告原因，不覆盖本地改动、不自动清理；
- `update-available`：只提示远程稳定分支存在不同提交，不自动切换。

需要升级时，必须从本仓库 `develop` 创建短期分支，选定不可变 commit，完成基础设施 Manifest 校验、消费端冒烟测试和真实任务试用，再只提交 submodule gitlink。升级失败时按协议记录证据并显式回退到上一个已验证 commit；禁止使用 `git submodule update --remote` 让任务在后台漂移。升级和回退的记录放在本仓库 `reviews/`，通用协议和工具留在基础设施仓库，便于其他项目小组复用。

共享基础设施当前提供哪些能力，完全以固定 submodule 提交中的 `manifest.yml` 为准。能力目录存在不等于能力可用，实际入口始终以 Manifest 为准；本仓库的项目规则不复制或维护第二份能力清单。

在启动判断或测试记录中注明实际 submodule commit；清单为空时记录“无可用共享能力”，不虚构能力 ID。能力为空只阻止相应共享能力调用，仍允许只读梳理上下文与缺失项。Manifest 不是权限系统或执行沙箱，已登记能力仍需核对输入、输出、依赖和副作用，并遵守本机工具授权。

遇到环境或权限错误，先只读诊断并记录；安装依赖、修复权限、删除临时文件或改客户端配置不是调查的默认动作。测试任务必须放到隔离测试 clone 并标记 `--test`，不得将合成用户确认或测试产出写入本仓真实任务。

## 写入和权限边界

- `vendor/` 下的基础设施 submodule 默认只读；版本升级是独立的、可评审的父仓库变更，不在普通任务中顺手修改；
- 项目资料、来源文件、作品、任务记录和评审记录写入父仓库；
- 不把客户机密、凭据、令牌、生产配置或未授权数据提交到仓库；
- Git commit、push、部署或正式发布必须具有相应用户授权，已有授权在其范围内继续有效；
- 不修改基础设施 submodule 内的文件来完成项目内容；
- 隐藏入口、目录结构和 Agent 指令不能替代实际权限控制。

## 作品与判断边界

作品存在不等于专业事实已经核验，工程检查通过不等于内容判断正确，评审记录存在不等于已经获得对外发布授权。专业判断、项目责任和发布确认必须由对应真人责任主体完成。

## 分支约定

- `main`：稳定、可供引用的资产仓库版本；
- `develop`：日常集成分支；
- `codex/feat-*`、`codex/fix-*`、`codex/chore-*`：从 `develop` 创建的短期分支；
- Chaos 全权负责本仓库的维护、合入和版本选择；
- 仓库为 public，进入仓库的项目事实、来源和表达资产必须符合公开或已确认的授权边界；
- `main` 应由服务端禁止删除和强制推送；服务端规则优先于本文件。

## 收口检查

完成任务前检查：

- 作品、任务、上下文、来源和评审记录的主位是否正确；
- 是否误把项目专属内容写入 submodule；
- submodule gitlink 是否指向预期 commit，且与实际 `HEAD` 一致；
- 是否提交缓存、凭据、环境文件或大型临时预览；
- 是否把专业确认或发布授权表达得超过实际状态；
- `git diff --check` 和 `git status` 是否清洁、准确。
