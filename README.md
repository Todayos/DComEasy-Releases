# DComEasy

![DComEasy — Windows OPC DA / DCOM 配置与诊断](assets/banner-zh-CN.svg)

<p align="center">
  <strong>简体中文</strong> · <a href="README.en.md">English</a>
</p>

<p align="center">
  <a href="https://github.com/Todayos/DComEasy-Releases/releases/latest"><strong>下载最新版本</strong></a>
  · <a href="docs/usage.md">使用指南</a>
  · <a href="https://github.com/Todayos/DComEasy-Releases/issues">问题反馈</a>
</p>

DComEasy 是面向工业现场部署、调试和维护的 Windows OPC DA / DCOM 配置与诊断工具。它将环境诊断、DCOM 权限配置、OPC DA 连接测试、点位监控、网络检测和诊断报告集中在一个界面中。

> [!IMPORTANT]
> DComEasy 是专有软件。本仓库仅用于官方版本发布、用户文档和问题反馈，不包含产品源代码。下载或使用软件即表示你同意发布包中附带的许可条款。

## 主要功能

- **配置诊断**：检查 DCOM、OPC Core Components、OPCEnum、权限和协议状态，并提供处理建议。
- **配置管理**：验证或创建本地 OPC 用户，预览并执行 DCOM 权限、身份验证级别和协议配置。
- **OPC DA 连接测试**：通过 ProgID 或 CLSID 验证远程服务器连接，展示网络检查、失败阶段、错误码和原始错误。
- **节点浏览与监控**：浏览 OPC 节点、查询完整 ItemID、读取点位并设置单点或批量刷新间隔。
- **网络检测**：检查目标连通性、端口、本机监听和防火墙状态，并按需添加本机入站规则。
- **诊断报告**：导出可选择、复制的 PDF 或单文件 HTML 报告，便于排查、交付和归档。
- **中英文界面**：支持简体中文和英文，并保留语言选择。

## 界面预览

### 配置诊断

![DComEasy 配置诊断](assets/screenshots/diagnosis-zh-CN.png)

### 执行配置

![DComEasy 执行配置](assets/screenshots/configuration-zh-CN.png)

### OPC DA 连接测试

![DComEasy OPC DA 连接测试](assets/screenshots/connection-zh-CN.png)

## 版本功能

| 功能 | 免费基础版 | 专业版 |
| --- | :---: | :---: |
| 配置诊断、用户验证和配置变更预览 | ✓ | ✓ |
| OPC DA 连接测试、节点浏览和单次读取 | ✓ | ✓ |
| 网络、端口和防火墙状态检查 | ✓ | ✓ |
| PDF 诊断报告 | 带免费版水印 | 无水印 |
| 创建本地 OPC 用户和执行 DCOM 配置 | — | ✓ |
| OPC 运行环境安装与修复 | — | ✓ |
| 点位持续刷新与批量监控 | — | ✓ |
| 自动添加防火墙规则 | — | ✓ |
| HTML 诊断报告 | — | ✓ |

## 系统要求

- Windows 桌面环境，可运行 x86 应用。
- 使用管理员权限安装和运行 DComEasy。
- 使用完整的离线安装包；安装包已包含所需的 .NET 运行时。
- 连接测试需要可访问的 OPC DA 服务器及该环境下有效的 OPC 用户信息。

## 下载与安装

1. 前往 [Releases](https://github.com/Todayos/DComEasy-Releases/releases) 下载最新的 `DComEasy-Setup-win-x86.exe`。
2. 以管理员身份运行安装程序。
3. 从开始菜单启动 DComEasy，并按提示以管理员身份运行。

安装包来自本仓库的 GitHub Releases。请勿从不明来源下载安装包，也不要只复制安装目录中的单个 EXE 文件。

更详细的操作步骤见[使用指南](docs/usage.md)。

## 问题反馈

提交问题前请先搜索[现有 Issues](https://github.com/Todayos/DComEasy-Releases/issues)。如果没有相同问题，请使用对应模板提交：

- [报告问题](https://github.com/Todayos/DComEasy-Releases/issues/new?template=bug_report.yml)
- [提出功能建议](https://github.com/Todayos/DComEasy-Releases/issues/new?template=feature_request.yml)

问题报告中请提供 DComEasy 版本、Windows 版本、复现步骤、预期结果和实际结果。上传截图或日志前，请移除账号、主机名、IP 地址和其他敏感信息；请勿提交密码或激活码。

## 版权与许可

Copyright © 2026 Todayos. All rights reserved.

DComEasy 为专有软件。本仓库公开可见不代表授予复制、修改、重新分发、反向工程或商业使用许可。软件的具体使用条件以发布包中附带的许可条款为准；第三方组件适用其各自的许可条款。
