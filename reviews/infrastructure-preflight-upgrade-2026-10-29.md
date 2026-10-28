# 基础设施版本预检与升级接入试用

- 状态：testing
- 消费端分支：`codex/feat-submodule-policy`
- 消费端接入提交：`dd8c074`
- 本记录提交：`b994e90`
- 旧 gitlink：`2252fadb8280cb1d9e7bd538cb86346452707a80`
- 候选/实际基础设施 commit：`d769c76de9ed31e8d02afd520ed59ac653bd07a0`
- 基础设施来源分支：`codex/feat-submodule-policy`
- 操作者：Chaos

## 目的

验证大工项目资产仓库能以通用方式恢复父仓库锁定的基础设施版本，检查 gitlink 与实际检出状态，并在远程稳定分支有差异时只提示、不自动漂移。该记录是消费端接入试用，不表示基础设施候选版本已经合入稳定 `main`，也不表示获得对外发布授权。

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
- Ruby Manifest 校验：本机未安装 Ruby，待 GitHub Actions 的 Ruby 3.3 环境补验。

## 结论与后续

本轮证明消费端可以固定并检查候选基础设施版本，且远程分支变化不会自动修改任务环境。候选基础设施提交仍在短期开发分支，后续需在基础设施仓完成评审、合入 `develop`，再由消费端建立新的升级任务验证 `develop` 提交；稳定后才考虑更新消费端 `main`。

若候选验证失败，按 [版本协议](../vendor/suanhai-team-external-expression-infrastructure/docs/submodule-consumer-versioning.md) 使用旧 gitlink 作为回退点，优先通过父仓 `git revert` 保留审计链。
