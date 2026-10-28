# 来源登记与事实状态

> **文档状态**：候选来源登记
> **整理日期**：2026-10-28
> **事实源仓库基线**：`suanhaitech/houzai@develop`，提交 `696d306`

本文件登记结构化上下文使用的来源，不复制来源正文。源仓库名称、分支、提交和相对路径用于复核定位；本文件不写入本机路径、受限源码、原始数据、账号或访问信息。

## 1. 来源登记

| 来源标识 | 源仓库 / 分支 / 提交 | 源文件相对路径 | 材料日期 | 事实状态 | 授权状态 | 本来源具体支持的表达 |
| --- | --- | --- | --- | --- | --- | --- |
| `houzai.project-context-index` | `suanhaitech/houzai@develop` / `696d306` | `docs/project/context/project-context-index.md` | 持续维护；当前索引早于 2026-10-23 | 项目上下文入口；部分状态需回源核对 | 仅支持本 public 仓库的脱敏摘要，具体 public 使用待确认 | 项目身份、信息主位、事实状态和更新规则 |
| `houzai.workstreams-index` | `suanhaitech/houzai@develop` / `696d306` | `kb/projects/dalianligong/workstreams/README.md` | 最近核对 2026-08-08 | 已建立主线索引；不是 10 月实时快照 | 具体内容的 public 使用待确认 | 三条主线、任务/产出目录职责和长期资产入口 |
| `houzai.promotion-workflow` | `suanhaitech/houzai@develop` / `696d306` | `kb/projects/dalianligong/workstreams/promotion-workflow.md` | 最近核对 2026-08-08 | 试运行流程 | 仅用于说明脱敏流程边界，具体发布待确认 | Issue 初始产出、项目审查、主线长期资产和对外报告的职责关系 |
| `houzai.engineering-preparation-index` | `suanhaitech/houzai@develop` / `696d306` | `kb/projects/dalianligong/workstreams/01_engineering_preparation/README.md`、`tasks.md`、`outputs.md` | 最近核对 2026-08-08 | 任务和产出状态可能已过期 | 具体环境细节和资源信息不公开 | 工程预备的范围、任务类型和证据限制 |
| `houzai.performance-index` | `suanhaitech/houzai@develop` / `696d306` | `kb/projects/dalianligong/workstreams/02_performance_special/README.md`、`tasks.md`、`outputs.md` | 最近核对 2026-08-08 | 部分材料已晋级，任务持续变化 | 具体数据、附件和算例按作品逐项确认 | 性能专项范围、预条件子和 `matrix-free` 任务边界、产出状态 |
| `houzai.architecture-index` | `suanhaitech/houzai@develop` / `696d306` | `kb/projects/dalianligong/workstreams/03_architecture_design/README.md`、`tasks.md`、`outputs.md` | 最近核对 2026-08-08 | MFEM 材料已晋级；SGSim 架构仍需验证 | 具体代码和图表按作品逐项确认 | 架构设计范围、MFEM 参考边界和 TensorFem/`matrix-free` 任务入口 |
| `houzai.external-report-2026-10-23` | `suanhaitech/houzai@develop` / `696d306` | `docs/affairs/external_reports/2026_10_23_dalianligong_sixth_biweekly/report.md` | 2026-10-23 | 对外汇报稿；阶段证据，未替代正式验收 | 作为源仓库的对外汇报稿使用；在本 public 仓库的二次发布范围待确认 | 三条方向的周期进展、证据、限制和下一周期安排 |
| `houzai.external-meeting-2026-10-23` | `suanhaitech/houzai@develop` / `696d306` | `kb/meetings/2026_10_23_dalianligong_sixth_external_biweekly/meeting_note.md` | 2026-10-23 | 会后整理稿，待参会各方核对 | 不能仅凭入库推断可公开；具体用途待确认 | 会议议程、讨论判断、待办和协作问题；不得写成自动生效的正式决策 |
| `houzai.grid-attachment-2026-10-23` | `suanhaitech/houzai@develop` / `696d306` | `docs/affairs/external_reports/2026_10_23_dalianligong_sixth_biweekly/attachments/SGSIm_网格分区实验.html` | 2026-10-23 | 阶段实验材料，有证据但未验收 | 算例、数据和图表的具体 public 使用待确认 | 约束感知分区、独立自由度、接口和限定条件下的阶段对照 |
| `houzai.solver-attachment-2026-10-23` | `suanhaitech/houzai@develop` / `696d306` | `docs/affairs/external_reports/2026_10_23_dalianligong_sixth_biweekly/attachments/SGSim_大规模结构求解.html` | 2026-10-23 | 阶段实验材料，有证据但未验收 | 算例、数据和图表的具体 public 使用待确认 | 区域分解、BDDC、直接法、迭代法、残差和零主元的限定条件观察 |
| `houzai.tensorfem-attachment-2026-10-23` | `suanhaitech/houzai@develop` / `696d306` | `docs/affairs/external_reports/2026_10_23_dalianligong_sixth_biweekly/attachments/SGSim_异构并行性能测试.html` | 2026-10-23 | 阶段验证材料，有证据但未验收 | 算例、硬件和图表的具体 public 使用待确认 | TensorFem CPU/GPU、多进程、分阶段计时和异构路径限制 |
| `houzai.external-report-2026-10-09` | `suanhaitech/houzai@develop` / `696d306` | `docs/affairs/external_reports/2026_10_09_dalianligong_fifth_biweekly/report.md` | 2026-10-09 | 历史对外汇报稿；不能替代最新状态 | 具体二次使用待确认 | 10 月 9 日阶段判断、三方向计划和历史语境 |
| `houzai.internal-context-2026-09-17` | `suanhaitech/houzai@develop` / `696d306` | `docs/project/context/current-state.md` | 快照 2026-09-17；历史状态 | 仅作历史背景，不能作为当前唯一依据 | 不作为 public 技术材料直接发布 | 三条主线的早期范围、历史风险和状态维护方式 |
| `asset.review-records` | 本资产仓库当前分支 | `reviews/` 下对应作品评审记录 | 逐项登记 | 以真人记录为准 | 决定具体作品能否用于特定受众和用途 | 事实核查、意见处理、受众和发布确认 |

## 2. 来源与内容状态的区分

“来源存在”只说明材料可以被定位。使用前还要分别判断来源内容的事实状态和授权状态：

| 事实状态 | 含义 | 表达方式 |
| --- | --- | --- |
| 已确认 | 有正式记录或责任主体明确确认，可在限定范围内作为事实前提 | 说明结论、来源和适用条件 |
| 有证据但未验收 | 有报告、日志、测试或会议材料，尚未完成正式技术审查或验收 | 写成阶段性观察并保留限制 |
| 草稿或计划 | 未来安排、候选方案或尚未执行的工作 | 写成拟、计划或候选 |
| 待核对 | 来源、数据、责任、适用条件或授权存在不确定性 | 不作为正式对外结论 |

授权状态至少包括：待确认、限定授权、已授权、过期或撤回。即使源文件本身来自对外汇报目录，也不能据此自动推导本 public 资产仓库的所有二次使用授权。

## 3. 重要主张的最小登记字段

制作作品或更新上下文时，对重要主张至少记录：

| 字段 | 记录内容 |
| --- | --- |
| 主张 | 要表达的事实、判断、计划或限制 |
| 来源标识 | 本表中的稳定来源 ID |
| 版本定位 | 仓库、分支、提交、相对路径和材料日期 |
| 事实状态 | 已确认、有证据但未验收、草稿/计划或待核对 |
| 适用条件 | 算例、输入、软件版本、硬件、进程/线程、正确性、残差、计时和限制 |
| 技术核对 | 谁负责事实和技术判断，核对是否完成 |
| 表达授权 | 面向什么受众、什么用途、授权主体和有效期限 |

缺少关键条件时，应降低表达强度，改写为阶段性观察、候选方案或待确认事项。

## 4. 更新规则

1. `houzai` 出现新的已确认报告、会议核对结果或长期资产时，先登记来源，再更新当前状态和作品。
2. 源仓库有冲突时保留冲突、来源、日期和待确认责任人，不静默覆盖已有摘要。
3. 10 月 23 日双周报、会议纪要及其附件的最新性不等于正式验收；后续来源进入后需要重新判断适用范围。
4. 来源登记不等于内容授权。作品发布前仍需在 `reviews/` 或相应确认记录中确认受众、用途、内容范围和期限。
