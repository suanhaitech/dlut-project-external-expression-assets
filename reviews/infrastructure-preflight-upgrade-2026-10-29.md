# 基础设施版本预检与升级接入试用

- 状态：accepted
- 消费端分支：`codex/feat-submodule-policy`
- 消费端接入提交：`dd8c074`
- 本记录提交：`b994e90`
- 旧 gitlink：`2252fadb8280cb1d9e7bd538cb86346452707a80`
- 候选基础设施 commit：`d769c76de9ed31e8d02afd520ed59ac653bd07a0`
- 已合入 develop 的基础设施 commit：`2797d8349b313b2f4dd17a8106c74ee03583475f`
- 基础设施来源分支：`develop`（通过基础设施 PR #4 合入）
- 操作者：Chaos

## 目的

验证大工项目资产仓库能以通用方式恢复父仓库锁定的基础设施版本，检查 gitlink 与实际检出状态，并在远程稳定分支有差异时只提示、不自动漂移。该记录是消费端接入试用，不表示获得对外发布授权。

## 实施内容

- 根 `AGENTS.md` 接入固定版本启动预检、显式升级和回退规则；
- `README.md` 改为以固定 submodule 提交中的 Manifest 作为能力唯一来源；
- `reviews/README.md` 增加升级/回退记录模板；
- 父仓库只更新 `vendor/suanhai-team-external-expression-infrastructure` 的 gitlink，没有复制 submodule 文件。

## 验证证据

### 固定版本离线预检

```powershell
py -3 vendor/suanhai-team-external-expression-infrastructure/tools/submodule-preflight/submodule_preflight.py `
  --root . `
  --path vendor/suanhai-team-external-expression-infrastructure `
  --skip-remote `
  --format text
```

结果：通过。父仓库 `HEAD` 中的 gitlink、index、submodule `HEAD` 和工作区均一致，固定 commit 对象可读取；远程检查明确标记为 `skip`，不宣称远程状态。

### 联网只读预检

```powershell
py -3 vendor/suanhai-team-external-expression-infrastructure/tools/submodule-preflight/submodule_preflight.py `
  --root . `
  --path vendor/suanhai-team-external-expression-infrastructure `
  --format text
```

结果：固定版本检查通过；远程 `main` 指针可读取，但与候选 commit 不同，整体状态为 `update-available`。工具没有执行 `fetch`、`checkout`、`update`、`reset`、提交或写配置。

### 基础设施候选回归

- 基础设施预检专项测试：5/5 通过；
- 基础设施完整 Python 回归：30 项通过，1 项因 Windows 符号链接权限跳过；
- 基础设施 `py_compile` 和 `git diff --check`：通过；
- Ruby Manifest 校验：本机未安装 Ruby；基础设施 PR #4 的 GitHub Actions Ruby 3.3 Manifest 检查通过。

### 合入 develop 后的消费端再验证

基础设施 PR #4 合入后，消费端 submodule 更新到 `2797d8349b313b2f4dd17a8106c74ee03583475f`，重新运行预检：

- 离线预检：父仓库 gitlink、index、submodule `HEAD` 和工作区一致，退出码 0；
- 联网预检：远端 `main` 指针与当前 `develop` 合入提交不同，状态为 `update-available`，没有自动切换或写入；
- 更新 submodule 前的父仓库提交：`4f01f8d927de8f47bda8013bfb8c9f9b93d0c237`；本次更新会产生新的父仓库提交。

## 结论与后续

本轮证明消费端可以固定并检查基础设施版本，且远程分支变化不会自动修改任务环境。基础设施预检工具已经合入 `develop`，大工消费端已固定并验证该稳定集成提交；后续可以在大工仓评审通过后合入消费端 `develop`，不直接修改 `main`。

若候选验证失败，按 [版本协议](../vendor/suanhai-team-external-expression-infrastructure/docs/submodule-consumer-versioning.md) 使用旧 gitlink 作为回退点，优先通过父仓 `git revert` 保留审计链。
