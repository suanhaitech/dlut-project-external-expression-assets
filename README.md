# 大工项目对外表达资产仓库

## 一、仓库定位

本仓库是大连理工项目小组维护的对外表达资产仓库，用于承载围绕项目形成的表达作品、必要素材、来源关联、任务记录和评审记录。

本仓库服务真实的项目沟通与交付需求。它可以承载项目概览、阶段进展、技术方案说明、培训材料、系列作品和其他面向外部受众的表达资产。仓库中的文件会随着真实使用逐步调整，不预设所有作品必须遵循同一媒介或同一生产流程。

当前状态：初始化基线。仓库为 public，已包含一份基于内部项目源仓库整理的脱敏候选上下文，但不包含源代码、原始项目资料、HTML 成品或已获对外发布授权的材料。进入仓库的项目事实、来源和表达资产必须符合公开或已确认的授权边界。

## 二、职责与边界

本仓库承担：

- 项目对外表达作品的创建、组织、修订和维护；
- 任务目标、受众、范围、来源和评审记录的保存；
- 作品与项目事实、技术成果和证据来源的必要关联；
- 成员在授权范围内使用本地 Agent 共同维护表达资产；
- 从真实任务中识别项目专属的表达工具和可回流的通用改进。

本仓库不承担：

- 不替代专业研发仓库维护代码、实验、数据和验证证据；
- 不替代 SuanhaiOS 的团队治理、成员、项目和权限职责；
- 不替代启元等知识仓库维护稳定团队知识主版本；
- 不因为作品存在、结构完整或视觉精美，就宣称技术能力已经成熟；
- 不因为文件进入本仓库，就表示已经通过专业评审或获得对外发布授权；
- 不把项目资料、客户资料或未授权来源复制到共享基础设施仓库。

作品、事实、证据、评审结论和发布授权必须分别判断。仓库归属、Git 提交或 Agent 生成不会自动产生团队共识、作者权益、专业结论或发布许可。

## 三、与相邻对象的关系

| 对象 | 主要承载位置 | 关系 |
| --- | --- | --- |
| 项目对外表达作品 | 本仓库 `works/`、`series/`、`courses/`、`books/` | 保存面向具体受众的表达资产 |
| 项目上下文与任务 | 本仓库 `context/`、`tasks/` | 说明为什么做、面向谁做、依据什么做 |
| 共享表达工程能力 | `vendor/suanhai-team-external-expression-infrastructure/` | 以 submodule 固定版本复用工具、技能、模板、Harness 和检查协议 |
| 专业研发成果 | 对应专业研发仓库 | 本仓库通过来源关联使用，不复制其主维护正文 |
| 团队治理与能力入口 | [SuanhaiOS](https://github.com/suanhaitech/suanhaios) | 本仓库应用适用的团队治理规则，不复制治理主定义 |

## 四、目录导航

| 目录 | 承载对象 | 当前用途 |
| --- | --- | --- |
| [`works/`](works/README.md) | 独立表达作品 | 第一项“大工项目概览与当前进展”HTML 汇报页的主要位置 |
| [`series/`](series/README.md) | 长期作品系列 | 组织多个具有持续表达关系的作品 |
| [`courses/`](courses/README.md) | 课程型表达项目 | 承载项目培训或教学型表达 |
| [`books/`](books/README.md) | 书籍型表达项目 | 承载具有系统性论述目标的长期项目 |
| [`tools/`](tools/README.md) | 项目专属辅助工具 | 放置只服务本项目、尚未适合回流基础设施仓的工具 |
| [`context/`](context/README.md) | 项目稳定上下文 | 记录目标、受众、阶段事实、来源边界和重要决定 |
| [`tasks/`](tasks/README.md) | 对外表达任务 | 记录一次工作的目的、范围、完成标准和责任信息 |
| [`reviews/`](reviews/README.md) | 评审与确认记录 | 保存意见、修订、待解决问题和真人确认 |
| [`vendor/`](vendor/suanhai-team-external-expression-infrastructure/README.md) | 共享基础设施 | 固定版本使用 Suanhai 团队通用表达工程能力 |

目录只是承载位置，不表示作品已经形成、质量已经确认或必须按顺序晋级。

## 五、基础设施 submodule

本仓库使用公开的基础设施仓库作为 submodule：

```text
vendor/suanhai-team-external-expression-infrastructure
```

父仓库中的 gitlink 是实际使用版本的唯一事实来源；`.gitmodules` 只记录路径和远程 URL。查询提交记录中固定的版本与本地实际检出状态：

```powershell
git ls-tree HEAD vendor/suanhai-team-external-expression-infrastructure
git submodule status --recursive
```

`git ls-tree` 显示父仓库提交中的版本；`git submodule status` 显示本地检出状态，以 `+` 开头表示本地与父仓库记录不一致。这里不另存第二份版本锁。实际可用能力始终以固定 submodule 提交中的 `manifest.yml` 为准；Agent 应从该文件读取能力 ID、类型、入口和依赖，本仓库不维护第二份能力清单。当前基础设施提供离线 HTML 汇报模板，但没有自动生成、预览或专用 HTML 检查器。

克隆本仓库后初始化 submodule：

```powershell
git clone git@github.com:suanhaitech/dlut-project-external-expression-assets.git
cd dlut-project-external-expression-assets
git submodule update --init --recursive
```

启动工作时先执行 `git submodule update --init --recursive` 恢复父仓库已经锁定的版本，再按基础设施仓库的 [消费端版本协议](vendor/suanhai-team-external-expression-infrastructure/docs/submodule-consumer-versioning.md) 做只读预检。预检可以提示远程稳定分支有更新，但不会改变工作树。

升级基础设施版本时，先在独立分支中试用明确的 commit，完成 Manifest 校验、消费端冒烟测试和真实任务验证后再提交父仓库 gitlink。记录旧/新 commit、实际能力清单、验证命令、结果和回退点到 `reviews/`。不要用 `git submodule update --remote` 让稳定版本跟随浮动分支；失败时按记录的旧 commit 显式回退。

## 六、本地 Agent 启动与验证

在已初始化 submodule 的仓库根目录启动会读取 `AGENTS.md` 的 Agent。根规则已接入基础设施的 [Bootstrap](vendor/suanhai-team-external-expression-infrastructure/docs/consumer-repository-bootstrap.md) 和 [Harness](vendor/suanhai-team-external-expression-infrastructure/docs/consumer-repository-harness-v0.1.md)。只读试用时输入：

```text
请梳理当前仓库中对外表达工作的启动条件、当前任务和可用共享能力；先不要修改文件。
```

Agent 应先理解项目上下文、列出固定 submodule Manifest 中的真实能力并说明缺失项。当前没有登记真实任务，只读请求下应报告缺少任务并停止作品生成。支持情况以实际 Agent 客户端测试为准；不自动读取 `AGENTS.md` 的客户端需要启动时显式要求读取根规则。

任务循环步骤见 [任务循环验证流程](vendor/suanhai-team-external-expression-infrastructure/docs/task-loop-validation.md)。历史空能力启动测试保存在 [原冒烟流程](vendor/suanhai-team-external-expression-infrastructure/docs/consumer-repository-smoke-test.md)，不能用旧结果代替当前版本测试。循环、专业内容正确性和发布授权分别验收。

获授权开始制作时，Agent 会先登记任务草案和任务号，再与用户对齐目标，持续制作/检查并收集反馈。任务状态以 `tasks/<编号>/task.json` 为准，`task.md` 为生成视图。以后可用“继续任务 <编号>”恢复进度；跨设备还需同步最新任务和产出文件。缺少 HTML 共享能力时先停在相应调用前，不伪造能力结果。

## 七、当前阶段和后续任务

当前阶段在候选项目上下文基础上接入可恢复任务循环；先在隔离测试 clone 验证，真实任务、HTML 成品和发布尚待后续验证。

后续第一项真实任务：

1. 在 `tasks/` 创建“大工项目概览与当前进展”任务说明；
2. 在 `context/` 记录受众、项目背景和获准来源；
3. 在 `works/` 创建第一份对外汇报 HTML；
4. 使用 submodule 中未来实现的 HTML 能力完成预览和检查；
5. 在 `reviews/` 记录评审、修订和真人确认；
6. 将具有跨小组复用价值的改进提取后回流基础设施仓库。
