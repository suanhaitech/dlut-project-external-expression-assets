# 来源登记与事实状态

本文件登记结构化上下文使用的来源，不复制来源全文。源仓库 Houzai 为 private 项目仓库；本 public 资产仓库只保存必要摘要和来源定位，不保存其源码、原始群聊、受限附件、账号、内网地址或原始性能数据。

| 来源标识 | 源仓库与版本 | 源路径 | 文档状态 | 本仓库的使用方式 |
| --- | --- | --- | --- | --- |
| `houzai.project-overview` | `suanhaitech/houzai@develop`，提交 `696d306` | `README.md`、`docs/project/context/project-context-index.md` | 项目级定位和上下文入口；索引本身标为 draft，最后核对早于本次快照 | 用于项目身份、范围、主线和事实状态规则，不复制正文 |
| `houzai.workstreams` | `suanhaitech/houzai@develop`，提交 `696d306` | `kb/projects/dalianligong/workstreams/` | 主线索引和任务/产出导航，持续维护 | 用于三条主线和产出生命周期摘要 |
| `houzai.external-report-2026-10-23` | `suanhaitech/houzai@develop`，提交 `696d306` | `docs/affairs/external_reports/2026_10_23_dalianligong_sixth_biweekly/report.md` | 对外汇报稿；正式发送和附件授权仍需按项目流程确认 | 用于 2026-10-23 阶段证据的候选摘要 |
| `houzai.external-meeting-2026-10-23` | `suanhaitech/houzai@develop`，提交 `696d306` | `kb/meetings/2026_10_23_dalianligong_sixth_external_biweekly/meeting_note.md` | 会后整理稿，待参会各方核对 | 用于阶段判断、下一步和待确认事项，不把整理稿写成最终决策 |
| `houzai.current-state-history` | `suanhaitech/houzai@develop`，提交 `696d306` | `docs/project/context/current-state.md` | 历史快照，早于 2026-10-23 | 只用于理解状态维护方式，不作为最新状态的唯一依据 |

## 事实状态与表达规则

- **已确认**：可以作为当前表达前提，但仍需检查时效和适用范围；
- **有证据但未验收**：可以作为阶段性证据和限制说明，不能写成正式验收结论；
- **草稿或计划**：只能用于“下一步计划”或“待确认事项”；
- **待核对**：不应直接进入对外结论或发布资产。

性能数值必须同时带有算例、代码/配置、硬件、进程/线程、计时和正确性口径。只要缺少其中关键条件，就降低表达强度，改写为限定条件下的阶段性观察。

## 来源更新规则

当 Houzai 出现新的已确认报告、会议核对结果或长期资产时，先更新来源登记和当前状态，再修订作品。源仓库有冲突时不静默覆盖本目录，保留冲突、来源和待确认责任人。
