# 有思 Yours

**你的训练，你的数据。**

有思是一款本地优先的训练记录 App，也是一套由用户掌控数据的长期训练系统。它帮助你记录计划、动作、训练历史和个人备注，并通过 Yours Vault 开放文件夹把这些记录连接到你自己的 AI agents 和工具链。

## 这个仓库是什么

YoursVault 是有思的公开发布、开放文件协议和 Agent Skills 仓库。主 App 源码位于
[`Maqiaogongmin/yours-app`](https://github.com/Maqiaogongmin/yours-app)。

本仓库公开：

- Android APK 下载说明与校验信息。
- App Store 下载入口。
- 版本更新日志。
- 隐私政策。
- 训练免责声明。
- Yours Vault 开放文件协议。
- 面向 AI agents / Codex 的 Yours Skills。

主 App、自托管同步服务与本仓库相互独立：

- 主 App：<https://github.com/Maqiaogongmin/yours-app>
- 自托管同步服务：<https://github.com/Maqiaogongmin/yours-sync-server>
- 发布资料、Vault 协议与 skills：当前仓库

## 长期训练闭环

有思的核心不只是记录一次训练，而是让长期数据持续参与下一轮计划：

1. 你自己编排计划，或让安装了 `yours-agent` skill 的 agent 根据目标、时间和器械生成计划。
2. Agent 输出可读 Markdown 和可导入的 `.plan.json`，放入 `Yours Vault/inbox/`。
3. 可用时通过 Yours CLI 验证和试运行；最终通过有思 App 的 inbox 导入完成校验和写入。
4. 在有思中记录真实训练，包括重量、次数、完成情况和备注。
5. 将训练记录整理到 Yours Vault，交给你选择的 agent 分析进展、瓶颈和执行情况。
6. Agent 据此调整下一轮计划，继续导入和执行。

```text
生成计划 -> 验证导入 -> 记录训练 -> Vault 沉淀 -> 分析调整 -> 下一轮计划
```

## 安装方式

### iPhone

有思已在 App Store 发布。

[<img src="assets/app-store-badge-zh-cn.svg" alt="在 App Store 下载有思" height="40">](https://apps.apple.com/cn/app/%E6%9C%89%E6%80%9D/id6772104994)

### Android

Android 版本通过 APK 分发。请优先从 [GitHub Releases](https://github.com/Maqiaogongmin/YoursVault/releases) 或有思官网下载安装包，并核对 SHA-256 校验值。

大多数近年 Android 手机建议选择：

- `Yours-android-arm64-v8a-1.11.2.apk`

较旧 Android 设备可尝试：

- `Yours-android-armeabi-v7a-1.11.2.apk`

模拟器或 x86_64 设备可使用：

- `Yours-android-x86_64-1.11.2.apk`

## Yours Vault

Yours Vault 是有思面向长期数据保存和外部工具协作的开放文件夹。它让训练数据可以被用户审阅、备份、迁移，并在用户授权后交给自己的工具分析。

当前原则：

- App 数据库由 App 内部管理。
- 外部工具不直接修改 App 内部数据库。
- 外部工具通过可审阅文件协作。
- 验证与试运行先于导入。
- 数据始终由用户掌握；服务器同步是可选的自托管能力。

## Agent Skills

本仓库提供一个给 AI agents / Codex 使用的 Yours Skill：

- `skills/yours-agent`：统一用于分析 Vault、创建或更新计划、补充自定义动作、准备 inbox 导入文件和执行可用的校验。

安装后可以让 agent：

- 根据目标、训练时间和器械生成计划。
- 检查计划 JSON 是否符合导入格式。
- 分析导出的训练记录和训练趋势。
- 把准备好的计划或动作文件放入 `inbox/`，等待验证和导入。

这些 skills 只描述文件协作流程，不包含用户训练数据、密钥或本机私有路径。CLI 是可选辅助；App inbox 导入器是最终权威校验层。详见 [`skills/README.md`](skills/README.md)。

## 核心功能

- **训练计划**：创建、归档和恢复自己的训练安排。
- **训练记录**：记录组、次、重量、休息、完成情况和个人备注。
- **标准记录 / 自由记录**：支持力量训练，也支持跑步、球类、拉伸等活动。
- **自定义动作**：维护适合自己的动作库。
- **多语言界面**：支持简体中文、English 和日本語，默认跟随系统。
- **本地优先**：默认不强制注册账号，训练数据默认保存在设备本地。
- **数据管理**：支持本地备份、Vault 导出、文件恢复和自托管服务器同步。

## 自托管服务器同步

如果你希望在 iPhone、iPad、Android 等设备之间同步训练计划和训练记录，可以自行部署有思自托管同步服务：

- GitHub 仓库：<https://github.com/Maqiaogongmin/yours-sync-server>

该服务用于部署到自己的 NAS、飞牛、家庭服务器或 VPS。有思不提供官方云账号系统，也不会托管你的训练数据；服务器地址、API 密钥、备份文件和同步事件都由你自己保存。

服务器同步使用 `protocolVersion: 2` 和 `identityMode: syncId`。它不是 Yours Vault，也不是 iCloud 自动同步；Vault 负责可审阅文件交换，服务器负责跨设备增量事件和快照兜底。

## 隐私

有思默认不要求账号。训练数据默认保存在设备本地。除非你主动导出、备份或分享，有思不会主动上传你的训练记录。

完整说明见 `privacy-policy.md`。

## 免责声明

有思是训练记录工具，不提供医疗建议。请根据自身情况合理训练，如有伤病或身体不适，请咨询专业人士。

完整说明见 `disclaimer.md`。

## 致谢

有思最早从开源健身项目 wger 的代码和实践中起步。对一个非程序员开发者来说，wger 像一套可靠的脚手架，让这个项目能够真正开始运行、学习和被改造。经过持续拆解、重写和产品方向调整后，有思逐步形成了本地优先、开放文件夹、Yours Vault 和个人 AI agents 工作流这些独立方向。感谢 wger 项目提供的开源基础与启发。

有思的数据自主理念也受到 Obsidian Vault 思路的启发：用户的数据应当尽可能可保存、可迁移、可被自己掌握。

## 源码许可证

有思主 App 采用 `AGPL-3.0-or-later`，并包含从 wger Flutter 项目沿用的
App Store 附加许可。许可证正文、来源审计和第三方归属以主 App 源码仓库为准。

## 反馈

如果你在测试中遇到问题，欢迎通过 GitHub 或官网提供的联系方式反馈。
