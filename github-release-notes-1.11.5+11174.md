# 有思 1.11.5 Android build 11174

本次发布更新 arm64-v8a Android APK，重点修复 Yours Vault inbox 和公共 Documents 导出问题，并同步当前代码健康治理成果。

## 更新内容

- 首次导出 Yours Vault 时自动建立 `Documents/有思/YoursVault/inbox`。
- 已授权目录下点击“导入 inbox”会直接读取文件，不再要求用户重复选择文件夹。
- 修复导入成功后仍提示 `vault input complete failed` 的错误误报。
- 修复重复导出产生 `manifest (1).json`、`manifest (2).json` 等副本的问题。
- 拆分 Android 平台桥接和高复杂度 Flutter 模块，增加自动化测试和发布健康门禁。

## 验收状态

- Flutter 静态分析通过，179 项测试通过，总覆盖率 71.85%，四个关键模块均超过 80%。
- Android Release 原生单测通过，lint 为 0 error、0 warning。
- Redmi M2007J3SC Android 16 真机：保留数据覆盖安装、冷启动、后台恢复、二次启动和 Yours Vault inbox 导入归档验收通过。
- 第二次导入未产生重复数据，未意外打开文件管理器，未发现 FATAL、ANR、PlatformException 或应用进程退出。

## APK

- 大多数 Android 手机：`Yours-android-arm64-v8a-1.11.5+11174.apk`
- SHA-256：`5f08c016838a823414ebc0f3594eac4f7f10f658a5fc5bdd3dea6dd0bbcf7db2`
- 对应公开源码 tag：`v1.11.5-public-source.1`

请优先覆盖安装，不要先卸载旧版，以免被 Android 系统删除本地数据。
