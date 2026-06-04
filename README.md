# 有思 Yours

**你的训练，你的数据。**

有思是一款本地优先的训练记录 App。它帮助你记录训练计划、动作、训练历史和个人备注，让训练数据尽量留在自己手里。

## 当前仓库内容

本仓库目前只用于发布和说明：

- Android APK 下载说明与校验信息。
- iPhone TestFlight 测试说明。
- 版本更新日志。
- 隐私政策。
- 训练免责声明。
- Yours Vault 数据协作方向说明。
- 面向 AI Agent / Codex 的 Yours Skills。

本仓库不包含有思 App 的完整源代码。等产品稳定后，再评估是否开放更多源码或开发文档。

## 安装方式

### iPhone

iOS 版本已通过 TestFlight 外部测试审核，可通过公开链接加入：https://testflight.apple.com/join/CXrh1a1e。

### Android

Android 版本通过 APK 分发。请优先从 [GitHub Releases](https://github.com/Maqiaogongmin/YoursVault/releases) 或有思官网下载安装包，并核对 SHA-256 校验值。

大多数近年 Android 手机建议选择：

- `Yours-android-arm64-v8a-1.11.0.apk`

较旧 Android 设备可尝试：

- `Yours-android-armeabi-v7a-1.11.0.apk`

模拟器或 x86_64 设备可使用：

- `Yours-android-x86_64-1.11.0.apk`

## Agent Skills

本仓库提供一组给 AI Agent / Codex 使用的 Yours Skills，适合想用外部工具读取训练数据、生成训练计划或通过 `inbox/` 准备导入文件的技术用户。

- `skills/yours-vault`：理解和使用 Yours Vault 开放文件夹协议。
- `skills/yours-cli`：使用 Yours CLI 执行导出、检查、试运行和导入前验证。
- `skills/yours-plan-author`：生成可读训练计划及配套 `.plan.json` 导入文件。

这些 skills 只描述文件协作流程，不包含用户训练数据、密钥或本机私有路径。详见 [`skills/README.md`](skills/README.md)。

## 核心功能

- **训练计划**：创建、归档和恢复自己的训练安排。
- **训练周整理**：手动标记训练周，计划仍可反复执行。
- **训练记录**：按单次训练查看时间戳，并可删除单次训练记录。
- **标准记录 / 自由记录**：标准记录适合力量训练的组、次、重量、休息；自由记录适合跑步、球类、拉伸等不按组记录的项目。
- **自定义动作**：维护适合自己的动作库，内置动作会按当前语言展示。
- **多语言界面**：支持简体中文与 English，默认跟随系统。
- **本地优先**：默认不强制注册账号，训练数据默认保存在设备本地。
- **数据管理**：支持本地备份、iCloud Drive 备份 / Vault 导出、文件恢复和自托管服务器同步。

## Yours Vault

Yours Vault 是有思面向长期数据保存和外部工具协作的开放文件夹设想。目标是让训练数据可以被用户审阅、备份、迁移，并在用户授权后交给自己的工具分析。

当前原则：

- App 数据库由 App 内部管理。
- 外部工具不直接修改 App 内部数据库。
- 外部工具通过可审阅文件协作。
- 验证与试运行先于导入。
- 数据始终由用户掌握；服务器同步是可选的自托管能力。

## 自托管服务器同步

如果你希望在 iPhone、iPad、Mac、Android 等设备之间同步训练计划和训练记录，可以自行部署有思自托管同步服务：

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

有思的早期探索曾受到开源健身项目 wger 的启发。感谢 wger 项目长期积累的健身记录思路与开源实践；当前发布包不包含 wger 品牌、数据或工程副本。

有思的数据自主理念也受到 Obsidian Vault 思路的启发：用户的数据应当尽可能可保存、可迁移、可被自己掌握。

## 反馈

如果你在测试中遇到问题，欢迎通过 GitHub 或官网提供的联系方式反馈。
