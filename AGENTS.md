# PrivaMask 网站仓库约束

## 提交与推送

- **提交信息只写版本号**（如 `v1.0.0`），不得包含改动说明、开发过程或任何操作细节；
  改动内容记录在本仓库 `docs/site-design.md` 的版本表中，不进提交信息。
- Git 身份固定使用产品身份：`privamask <privamask@weibaba.fun>`（仓库级配置，勿改回个人身份）。
- 分支流程：日常改动在 `dev` 分支进行 → 验证后合并 `main` 发布 → 建 `release/vX.Y.Z` 分支 +
  轻量标签 `vX.Y.Z`（无标签消息）→ 切回 `dev`。
- 仅允许推送本网站仓库；应用源码严禁推送 GitHub。NAS 备份推送不受限。

## 站点红线

- 纯静态、零追踪：不引入统计/分析、外部字体与 CDN 资源、表单、Cookie、任何第三方请求。
- 仓库不得出现用户数据、操作日志、凭据、本机路径等任何非公开信息。

## 口径管理

- 产品口径（功能、格式、版本与分阶、隐私事实）只能来自应用仓库权威文件
  （README、docs/requirements.md、PRIVACY.md、THIRD_PARTY_NOTICES），禁止编造；
- 口径变更先回写 `docs/site-design.md`，再改页面代码。
