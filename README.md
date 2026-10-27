# 大工项目对外表达资产仓库

## 一、仓库定位

本仓库是大连理工项目小组维护的对外表达资产仓库，用于承载围绕项目形成的表达作品、必要素材、来源关联、任务记录和评审记录。

本仓库服务真实的项目沟通与交付需求。它可以承载项目概览、阶段进展、技术方案说明、培训材料、系列作品和其他面向外部受众的表达资产。仓库中的文件会随着真实使用逐步调整，不预设所有作品必须遵循同一媒介或同一生产流程。

当前状态：初始化基线。仓库为 public，暂不包含真实项目资料、HTML 成品或已获对外发布授权的材料。进入仓库的项目事实、来源和表达资产必须符合公开或已确认的授权边界。

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

当前固定提交：

```text
28a2e61d472af8983aef36ca771fc30580a247db
```

父仓库中的 gitlink 是实际使用版本的唯一事实来源；`.gitmodules` 只记录路径和远程 URL。当前基础设施提交的 `manifest.yml` 中 `capabilities` 为空，因此本次初始化只验证 submodule 的发现路径和版本关系，不能宣称已经具备 HTML 自动制作能力。

克隆本仓库后初始化 submodule：

```powershell
git clone git@github.com:suanhaitech/dlut-project-external-expression-assets.git
cd dlut-project-external-expression-assets
git submodule update --init --recursive
```

升级基础设施版本时，先在独立分支中试用明确的 commit，完成真实任务验证后再提交父仓库 gitlink。不要用 `git submodule update --remote` 让稳定版本跟随浮动分支。

## 六、当前阶段和后续任务

当前阶段只完成资产仓库初始化，不制作 HTML 成品，不部署，不发布。

后续第一项真实任务：

1. 在 `tasks/` 创建“大工项目概览与当前进展”任务说明；
2. 在 `context/` 记录受众、项目背景和获准来源；
3. 在 `works/` 创建第一份对外汇报 HTML；
4. 使用 submodule 中未来实现的 HTML 能力完成预览和检查；
5. 在 `reviews/` 记录评审、修订和真人确认；
6. 将具有跨小组复用价值的改进提取后回流基础设施仓库。
