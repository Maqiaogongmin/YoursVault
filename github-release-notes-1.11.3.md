# 有思 1.11.3 Android

本次发布将 Android APK 更新到当前 1.11.3 主线。

## 更新内容

- 同步数据管理操作状态、备份诊断和同步流程改进。
- 保留 Android 系统栏、真机大字体按钮、公共 Documents 导出和 Yours Vault 适配。
- 继续使用服务器同步协议 v2：`protocolVersion: 2`、`identityMode: syncId`。
- 覆盖安装旧版时保留本地训练数据、服务器地址和 API 配置。
- Android 不显示 iCloud 入口；跨端同步请使用自托管服务器或备份包。

## APK 选择

- 大多数 Android 手机：`Yours-android-arm64-v8a-1.11.3.apk`
- 较旧 Android 设备：`Yours-android-armeabi-v7a-1.11.3.apk`
- Android 模拟器或 x86_64 设备：`Yours-android-x86_64-1.11.3.apk`

请下载后核对 `SHA256SUMS.txt`。
