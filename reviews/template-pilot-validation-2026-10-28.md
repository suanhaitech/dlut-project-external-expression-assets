# HTML 模板套用试点验证

## 范围

本记录只说明消费端 Agent 对共享模板的隔离套用验证，不是大工项目技术事实、专业验收或对外发布授权。测试任务和 HTML 作品留在仓库外的隔离 clone，没有写入本仓库。

- 消费端测试分支：`codex/feat-html-template`
- 消费端测试提交：`67d01bb79eab27cdb28f14dba2e8de94420e3370`
- 基础设施模板提交：`2252fadb8280cb1d9e7bd538cb86346452707a80`
- 测试任务：`EXPR-20261028-496dedf9`，`mode: test`
- 测试来源：消费端公开 `README.md`、`AGENTS.md`

## 已观察结果

独立 Agent 从根规则和固定 Manifest 发现了 `html.project-report-v1`，在隔离 clone 中完成：

1. 登记任务草案并提出受众、范围和交付形式问题；
2. 根据明确标记的合成确认完成对齐并开始制作；
3. 将模板复制到 `works/<任务号>/v001/`，填充 34 个 `data-slot`；
4. 保留 `README.md`、`LICENSE`、`NOTICE`、`template.yml`、`styles.css` 和 `report.css`；
5. 登记首版 HTML 进入 `review`，没有记录完成或发布授权。

隔离任务的作品摘要为：

`b97deccb8268a4e0dd6bbf599e750e917da910e483627656fa7894f52fb03874`

## 检查结果

- Python 标准库 HTML 解析通过；
- `#top`、`#overview`、`#progress`、`#evidence`、`#next` 锚点有效；
- 页面没有外部网络引用；
- `template.yml` 保留 `html.project-report-v1`、`offline: true` 和空的 `network_dependencies`；
- 模板元数据、许可证、NOTICE 和本地 CSS 文件存在且与模板源一致；
- 任务 `validate` 和 `git diff --check` 通过；
- 测试没有修改 `vendor/` 或 `context/`，没有安装依赖、提交、推送或部署。

## 结论和限制

这次验证证明了固定 submodule 提交中的模板可以被消费端 Agent 发现、复制、填充和记录，满足首轮模板试点的工程闭环。它没有验证真实项目内容、视觉质量、浏览器多尺寸截图、专业事实正确性或发布授权；HTML 自动生成器、预览工具和确定性 HTML 检查器仍未实现。

后续真实任务应在新的任务编号下登记，明确受众、允许来源和发布边界，不能直接把本次 `mode: test` 产出当作项目交付物。
