# DComEasy v2.0.1

## 主要更新

- 新增多点监测任务：任务可先创建、后添加点位；点位支持服务器树批量选择，任务列表支持手动刷新。
- 可随时打开任务的全部点位实时趋势，不必启动检测或先设置触发规则。完整配置数值阈值后，任务按统一周期批量采样；触发时自动归档包含全部点位的 PDF 报告和 CSV 数据。
- 新增 OPC DA 服务器发现，以及可加密导入、导出的 `.dc` 配置模板（Pro／企业版）。
- 改进趋势图、任务操作和报告排版，并修复部分界面翻译、刷新图标及连接／采样异常提示。
- 更新中英文演示动图和使用指南；README 提供三个免费 Pro 激活码，首次激活和使用截止日均为 2026-12-31。

## 演示

以下画面均从 2.0.1 当前程序重新采集；连接与监测数据为示例数据。

![DComEasy 2.0.1 中文演示](https://raw.githubusercontent.com/Todayos/DComEasy-Releases/main/assets/quick-start-v2.0.1-zh-CN.gif)

[View the English demo](https://github.com/Todayos/DComEasy-Releases/blob/main/assets/quick-start-v2.0.1-en-US.gif)

## 安装

下载 `DComEasy-Setup-v2.0.1.exe`，以管理员身份运行。安装包包含所需的 .NET 运行时；程序以 32 位进程运行，用于兼容 OPC DA 和相关 COM 组件。

升级前请关闭 DComEasy；保留安装器默认显示的原目录即可原地升级。

## 文件校验

```text
SHA-256  c57a5bca3bba94010f6932adb12709a9212d1ad904192f1760c1dbb9e1867447
```

请只从本仓库的正式 Release 下载安装包。
