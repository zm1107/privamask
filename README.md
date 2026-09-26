<div align="center">

<img src="assets/img/logo-170.png" width="170" alt="数隐通 PrivaMask">

# 数隐通 PrivaMask

**批量脱敏，留痕可还原。**

Windows 本地数据脱敏工具：批量处理 Excel、CSV、Word 文件中的敏感信息

**🛡️ 全程本地零上传 &nbsp;·&nbsp; 📊 xls · xlsx · csv · doc · docx &nbsp;·&nbsp; 🎭 遮蔽 + 虚构双模式 &nbsp;·&nbsp; ↩️ 位置级还原 &nbsp;·&nbsp; 📤 映射规则导出**

[官网 privamask.weibaba.fun](https://privamask.weibaba.fun) · [从微软商店下载](https://apps.microsoft.com/detail/9P75XG3KTHR8) · [隐私政策](https://privamask.weibaba.fun/privacy/)

</div>

## 支持格式

| 类型 | 格式 | 说明 |
|---|---|---|
| Excel | xlsx / xls | xlsx 完整保留格式与样式；xls 优先经本机 Excel 保格式读写，无 Excel 时降级读取并输出 xlsx |
| CSV | csv | 编码自动检测（UTF-8 / GBK / UTF-8-BOM），输出保持原编码 |
| Word | docx / doc | docx 处理正文、表格、页眉页脚、文本框；doc 经本机 Word 转存后处理，输出 docx |

公式单元格跳过，仅处理字面值。

## 版本

| 版本 | 说明 |
|---|---|
| 公开测试版 v1.0.0 | 全部功能开放，60 天全功能、全免费 |
| 免费版 / 收费版 | 规划中，分阶方案以后续商店页面为准 |

## 功能亮点

- **脱敏流程**：文件夹批量选择、递归扫描，多文件并行（默认 2 线程，可配置 1–8）；列名关键词 + 内容抽样双通道自动识别，确认对话框中可逐项人工改判；逐文件结果与带时间戳的处理日志（可复制、清空、导出）
- **遮蔽 + 虚构双模式**：星号遮蔽（默认）支持自定义模板，`#` 按位保留原文（如 `13812345678` → `138****5678`）；假数据替换在同任务内同值同假名，保证统计口径一致
- **还原双通道**：「从映射文件还原」与「从历史任务还原」并存；位置级映射按「文件 / 工作表 / 行 / 列」坐标写回原文，还原前校验文件 hash
- **规则管理**：内置 7 类敏感字段（公司名称、人员名称、手机号码、账户号码、社会信用代码、银行账号、身份证号）；规则存于本机 SQLite，界面化增删改与启停；映射规则可导出 xlsx 留存

## 隐私

数隐通**全程本地处理**：无网络请求、无遥测、无统计、无账号、无 Cookie；源文件只读不改。详见[隐私政策](https://privamask.weibaba.fun/privacy/)。

## 合规声明

请在合法合规的前提下使用本工具：使用者应自行确认对所处理数据的合法权益与数据安全义务。

## 关于本仓库

本仓库托管数隐通（PrivaMask）官方网站（privamask.weibaba.fun）源码：纯静态、零追踪（无统计、无 Cookie、无外部请求、无表单），站点口径以 [`docs/site-design.md`](docs/site-design.md) 为准；产品口径以应用仓库为权威。

## 致谢

数隐通基于以下优秀开源组件构建（随软件分发，清单以应用仓库许可声明为准），向原作者与开源社区致谢：

| 项目 | 用途 | 许可证 |
|---|---|---|
| Python / PySide6 | 运行时与图形界面 | PSF / LGPL-3.0 |
| openpyxl / xlrd | xlsx / xls 读写 | MIT |
| python-docx | docx 处理 | MIT |
| pywin32 | Word / Excel COM 桥接 | PSF |
| chardet | CSV 编码检测 | LGPL-2.1 |

> 组件与许可证以应用仓库 `THIRD_PARTY_NOTICES` 及打包时的实际依赖为准。
