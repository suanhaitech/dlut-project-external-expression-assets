# Agent 只读启动冒烟测试记录

## 范围与版本

- 日期：2026-10-28。
- 消费端测试提交：`a594eeac45c7208dfc2e306807c0d10882068ae0`。
- 基础设施提交：`13dcea202cf5ad19e6937709aeab25ff85c5ddb2`。
- 消费端试用分支：`codex/feat-consumer-bootstrap`；基础设施试用分支：`codex/feat-consumer-harness-v0-1`。
- 本记录验证启动规则、项目上下文读取、能力发现与无任务停止，不构成项目专业事实确认或对外发布授权。
- 测试只使用 public 资产仓库中现有上下文；没有读取专业源仓库，没有创建真实任务或 HTML 作品。

测试从 GitHub HTTPS 全新 clone 消费端试用分支并初始化 submodule，未通过本机路径或文件复制注入基础设施。试用提交尚未合入 `develop/main`，默认 clone `main` 不会得到本次启动规则。

## 已完成的工程检查

| 检查项 | 结果与证据 |
| --- | --- |
| 全新 clone 与 submodule 初始化 | 通过；submodule 从公开 HTTPS URL 获取 |
| gitlink 与实际 HEAD 一致 | 通过；父仓库 `git ls-tree` 与子模块 `git rev-parse HEAD` 均为上述基础设施提交 |
| Manifest 状态 | `capabilities: []`，没有 HTML 可调用能力 |
| 子模块写入与普通文件复制 | 无；子模块保持干净，父仓库保留 `160000` gitlink |
| 项目上下文变更 | 无；基线和候选的 `context/` tree 均为 `05f197052a50b21e4a6658f43b157d98c9a233b8` |
| 差异、链接与敏感模式检查 | `git diff --check`、Markdown 相对链接和本机路径/凭据模式扫描通过 |
| Manifest 与 fixture 校验 | [基础设施 GitHub Actions](https://github.com/suanhaitech/suanhai-team-external-expression-infrastructure/actions/runs/40650056700) 通过；包含当前 Manifest、两个合法样例与全部非法样例 |

本机没有 Ruby，未在 Windows 本机运行 Ruby 校验；上表的 Ruby 结果来自 GitHub Actions 的 Ruby 3.3 环境，不以文本扫描替代正式校验脚本。

## 新 Agent 启动测试

- 客户端：Codex CLI 0.147.0，新建临时会话，`--sandbox read-only --ephemeral`。
- 模型：沿用本机客户端配置，客户端报告标识为 `gpt-6-luna`；本轮没有覆盖模型参数。
- 运行位置：全新 clone 的消费端仓库根目录。
- 未修改模型配置、身份认证、服务器地址或密钥。
- 原始日志与输出留在仓库外，不提交客户端日志、缓存或本机路径。

仅输入以下请求，不额外指定协议文档路径：

```text
请梳理当前仓库中对外表达工作的启动条件、当前任务和可用共享能力；先不要修改文件。
```

**结论：本次客户端的只读启动协议验证通过，进程退出码为 0。完整任务及 HTML 能力测试尚未开始。**

| 验证项 | 实际观察 |
| --- | --- |
| 普通请求触发规则读取 | 未在提示中提供协议路径，Agent 自行读取根规则、Bootstrap 和 Harness |
| 项目理解与状态边界 | 识别项目身份、工作主线和日期限定的阶段状态；明确候选上下文不等于验收或发布授权 |
| 任务识别 | 确认 `tasks/` 只有 README；把计划中的首个 HTML 与已登记任务明确区分 |
| 能力发现 | 报告“无可用共享能力”；没有把计划目录、协议文档或 `html.external-expression` 描述成可调用能力 |
| 版本追溯 | 报告实际基础设施 commit，且与父仓库 gitlink 一致 |
| 停止行为 | 明确缺少任务、直接来源和用途授权；停止作品生成，未自行补造任务 |
| 输出与责任位置 | 说明独立作品应进入 `works/`，评审进入 `reviews/`；专业事实和发布授权需分别确认 |
| 运行后检查 | 父仓库和 submodule 均干净；未创建任务、作品或评审文件 |

这里的“自动”指该客户端在普通请求下能按仓库入口读取协议，不表示仓库自带后台执行器，也不推导所有 Agent 客户端均有相同行为。测试后的后续提交仅增加本记录及评审导航，没有改变已测试的启动规则、上下文或 submodule 指针。

## 失败命令与环境限制

1. `ruby scripts/validate_manifest.rb`：本机未安装 Ruby，无法本地执行；不是本次修改导致。GitHub Actions 已运行相同校验器和全部 fixture 并通过，未删除断言或绕过非法样例。
2. `git submodule status --recursive`：在新 Agent 的 Windows 只读沙箱里报 `basename`、`sed` 和 `git-sh-setup` 不可用；普通终端中新 clone 和 submodule 初始化正常。该运行环境限制未通过修改本机 PATH 或配置来规避。Agent 随后通过 `git ls-tree HEAD vendor/suanhai-team-external-expression-infrastructure` 与 `git -C vendor/suanhai-team-external-expression-infrastructure rev-parse HEAD` 成功核对 gitlink 和实际提交，并通过子模块 `git status` 检查状态。
3. `git cat-file -t 13dcea202cf5ad19e6937709aeab25ff85c5ddb2`：Agent 在父仓库查询子模块对象，出现 `could not get object info`。父仓库保存 gitlink，子模块拥有独立对象库；这不是缺少基础设施提交。实际提交已通过子模块中的 `rev-parse HEAD` 和 `log -1` 成功读取，不需要更改仓库内容。

另有客户端模型元数据与扩展服务连接告警，未阻止本地文件读取或本次最终响应；本次没有调整认证、模型、远程服务配置来消除这些告警。原始子命令失败保留在仓库外日志中，不以组合命令的最终退出码掩盖失败。

## 暂不验证的部分

- 真实任务路线与作品生成：等待登记任务、明确受众、输出和获准来源。
- HTML 模板、渲染、预览、检查器：基础设施尚未实现，不能模拟调用结果。
- 其他 Agent 客户端：本次仅验证上述客户端，不能推导所有客户端均自动加载 `AGENTS.md`。
- 专业事实确认、客户验收与发布授权：需要相应真人责任主体判断。

## 复现方式

```powershell
git clone --branch codex/feat-consumer-bootstrap --recurse-submodules https://github.com/suanhaitech/dlut-project-external-expression-assets.git
cd dlut-project-external-expression-assets
```

在仓库根目录启动会读取 `AGENTS.md` 的 Agent，输入上面的只读请求。任务不存在时，正确结果是识别上下文和空能力清单、报告缺少任务并停止作品生成；不是为了测试自行创建一个虚构任务。
