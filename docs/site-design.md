# 数隐通（PrivaMask）官方网站 — 需求与设计说明

#官网 #站点设计 #PrivaMask

> 状态：已定稿（v1.0.0） · 日期：2026-09-25
> 本文档先于代码存在；任何口径变更须先回写本文档，再改页面代码。

## 1. 需求

为数隐通（PrivaMask，Windows 本地数据脱敏工具）建设官方产品站，结构与写法惯例参考
同作者的 PassGone 与 ExifMate 网站仓库（二者仅作只读参考，文案与数据不复制），
品牌视觉自应用源图标派生。

- **域名与口径**：`https://privamask.weibaba.fun`；反馈邮箱 `feedback@weibaba.fun`；© 2026 Weibaba（全局规范第 12 条）。
- **发布方式**：公开 GitHub 仓库（`privamask`）→ Cloudflare Pages 静态托管，生产分支 `main`，仓库根即站点根。
- **隐私红线（硬性）**：纯静态、零追踪——无统计/分析、无任何外部请求（无 CDN 字体、无外链图片/JS）、
  无 Cookie、无表单、无服务端代码；仓库内不得出现用户数据、操作日志、凭据或本机路径。
- **下载入口**：微软商店 `https://apps.microsoft.com/detail/9P75XG3KTHR8`（唯一权威渠道，应用 ID 见 ADR-010）。
- **双语**：中文主站 `/` + 英文版 `/en/` 逐节对应；隐私政策 `/privacy/` 中英同页切换。

### 1.1 产品口径来源（权威文件清单，禁止编造）

| 站点内容 | 来源（应用仓库，本地路径见项目内部文档） |
|---|---|
| 功能、格式、流程、还原、规则口径 | `docs/requirements.md`（FR1–FR9）、`docs/design.md`（§6 导航与还原双通道） |
| 特性徽章行、一句话定位 | 任务口径（v1.0.0 发布协调口径）+ `docs/requirements.md` §1/§2 |
| 版本与分阶（公测 60 天全功能免费；免费/收费规划中） | 任务口径（v1.0.0 发布协调口径） |
| 隐私政策全部事实 | 任务口径（协调者给定事实清单）；应用仓库 `PRIVACY.md` 产出后同步核对 |
| 品牌配色与图标 | 应用仓库 `store/ico/app_icon.png`（512×512 唯一设计源头） |

注：应用仓库 `README.md` 与 `PRIVACY.md` 在本版建站时仍由并行助手撰写中（README 现为骨架），
站点先行按任务口径起草；待其定稿后须逐项核对，如有出入以应用仓库为准并回写本文档。

## 2. 品牌视觉（自源图标派生）

源图标：`store/ico/app_icon.png`（512×512，蓝底圆角方块 + 白色盾形 + 三枚绿色花号——
「盾牌护数 + 星号遮蔽」）。

| 用途 | 变量 | 值 | 来源 |
|---|---|---|---|
| 主色（品牌蓝） | `--accent` | `#2F6FB3` | 任务口径（应用内置图标蓝） |
| 深蓝（标题/渐变中段） | `--accent-deep` | `#075293` | 图标底色实测众数 |
| 主色 hover | `--accent-d` | `#255C96` | 主色加深 |
| 深夜蓝（渐变起点） | `--hero1` | `#052644` | 深蓝加深派生 |
| 绿花（CTA/点缀） | `--leaf` | `#0EB490` | 图标花号实测众数 |
| 绿花 hover | `--leaf-d` | `#0B9375` | 绿花加深 |
| 正文墨色 | `--ink` | `#17293C` | 偏藏青深墨 |
| 背景 | `--bg` | `#F4F7FA` | 冷灰蓝底 |

Hero 渐变：`#052644 → #075293 → #2F6FB3`（135°）。
字体：系统字体栈（Microsoft YaHei UI / Segoe UI / system-ui），不引用任何外部字体。

### 2.1 图标派生（脚本化，禁止各尺寸手改）

派生脚本 `tmp/derive_icons.py`（Pillow，conda 环境 `privamask`；`tmp/` 不入库，配方记录于此）：
读源图标 → LANCZOS 缩放输出——

| 产物 | 尺寸 |
|---|---|
| `assets/img/logo.png` | 512×512（Hero 与 og:image） |
| `assets/img/logo-170.png` | 170×170（README 头部） |
| `favicon.png` | 128×128 |
| `apple-touch-icon.png` | 180×180 |
| `favicon.ico` | 16 / 32 / 48 三档 |

色值取样脚本同目录 `tmp/sample_colors.py`（背景众数 `#075293`、花号众数 `#0EB490`）。

## 3. 站点结构与页面结构

```
/                     中文主站（lang=zh-CN）
/en/                  English（lang=en）
/privacy/             隐私政策（中英同页切换，onclick 切换 data-lang，无框架无存储）
/assets/style.css     全站唯一样式
/assets/img/          logo.png（512，og:image）、logo-170.png
/favicon.ico|.png、/apple-touch-icon.png   全部由源图标派生
/robots.txt /sitemap.xml /_headers /.well-known/security.txt
README.md AGENTS.md docs/site-design.md .gitignore
```

主站信息架构（锚点）：**Hero（居中 logo + slogan「批量脱敏，留痕可还原」+ 一句话定位 +
特性徽章行 + 下载按钮 + 版本卡）→ 功能区 `#features`（四块：脱敏流程 `#workflow` /
双模式 `#modes`（含遮蔽模板演示）/ 还原双通道 `#restore` / 规则管理 `#rules`）→
内置 7 类 `#builtin`（字段芯片行）→ 支持格式 `#formats`（5 格式芯片 + 公式跳过注）→
隐私承诺块（链接 `/privacy/`）→ 页脚（产品/支持/法律四列，GitHub 占位 `#`）**。

- 版本卡口径：公开测试版 v1.0.0——60 天全功能、全免费；免费版/收费版规划中。
- 隐私页节结构（中英对应）：核心承诺 → 1 处理方式 → 2 数据存放位置 →
  3 含原文文件的保管责任 → 4 源文件只读 → 5 卸载与残留 → 6 联系 → 7 关于本网站；
  页尾注明「本文与应用内 PRIVACY.md 同步，以应用仓库为权威」。
- 赞助位：暂缺收款码资产，本版未设；资产提供后在主站与 README 尾部补齐。

## 4. 零追踪实现要点

- 唯一 JS 为隐私页语言切换的两个 `onclick`（改 `data-lang`，无存储、无请求）。
- 外链仅微软商店与 `mailto:`，均需用户主动点击；无 iframe、无字体外链、无统计。
- `_headers` 输出 X-Content-Type-Options / X-Frame-Options / Referrer-Policy / Permissions-Policy。

## 5. 部署（Cloudflare Pages，用户侧操作步骤）

1. **GitHub 建仓**：在 GitHub 创建空仓库 `privamask`（与本地目录同名；不要初始化 README/.gitignore）。
2. **关联远程并推送**（仓库地址以实际账号为准，配置前与用户确认）：
   `git remote add origin git@github.com:<账号>/privamask.git`
   `git push -u origin main`
3. **Cloudflare Pages**：Dashboard → Workers & Pages → Create → Pages → Connect to Git →
   选 `privamask` 仓库 → 生产分支 `main` → 构建命令留空 → 输出目录 `/` → Save and Deploy。
4. **自定义域**：Pages 项目 → Custom domains → 添加 `privamask.weibaba.fun`；
   按提示在 DNS 处为 `privamask` 添加 CNAME 指向 `<项目名>.pages.dev`
   （若 weibaba.fun DNS 托管在 Cloudflare 则自动完成）。
5. **验证**：访问 `https://privamask.weibaba.fun/`、`/en/`、`/privacy/`，
   并用浏览器开发者工具确认无任何第三方请求。
6. （可选，推荐）**NAS 备份远程**：按全局规范 `rules/website.md` 15.2 的口径配置 NAS 备份远程（命名 `nas`，`<产品名>_website` 后缀仓）后推送。

## 6. 版本

| 日期 | 版本 | 说明 |
|---|---|---|
| 2026-09-25 | v1.0.0 | 首版上线：中文主站 `index.html`（Hero + 功能四块 + 7 类字段 + 格式 + 隐私承诺 + 页脚）；英文版 `en/index.html`（逐节对应）；隐私政策 `privacy/index.html`（中英双语）；全站样式 `assets/style.css`；品牌图 `assets/img/logo.png`、`assets/img/logo-170.png`；`favicon.ico`、`favicon.png`、`apple-touch-icon.png`；`robots.txt`、`sitemap.xml`、`_headers`、`.well-known/security.txt`、`.gitignore`；`README.md`、`AGENTS.md`、本文档 |

> 注：提交信息仅含版本号，改动说明只记录于本表。

| v1.0.1 | 2026-09-26 | README 致谢表 PyQt6→PySide6（LGPL-3.0），随应用框架迁移同步（应用仓库 ADR-014） |
| v1.0.2 | 2026-09-26 | 反馈邮箱统一为 feedback@weibaba.fun（全局规范第 12 条修订），全站与隐私页同步 |
