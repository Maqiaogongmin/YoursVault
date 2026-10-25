# 有思 1.11.7 Android build 11178

Android 与 HarmonyOS 同步到 iOS 1.11.7 业务代码。

## 更新内容

- 修复同一训练中重复同名动作的记录互相覆盖，每个动作块独立保存训练组。
- 替换动作后保存自定义组数、次数、重量、休息时间和动作快照，重新打开后继续训练。
- 同步更新备份与服务器同步的动作身份和训练快照。
- 修复训练记录标题中部分中文字形重影。

## 验证

- Flutter 静态分析通过，182 项测试通过。
- Android 16 / Pixel 8 arm64 模拟器覆盖安装、冷启动、四个主页面、Vault 导入导出、训练记录和后台恢复通过。
- 同名卧推动作分别保存 40 kg 与 55 kg；替换为深蹲后 70 kg、6 次、休息 30 秒在冷启动后保留，并完成保存。
- 未发现 Android/Flutter fatal 日志；本次未进行 Android 真机验证。

## 下载与源码

- APK：`Yours-android-arm64-v8a-1.11.7+11178.apk`（arm64-v8a）。
- Android `versionCode=13178`，显示版本 `1.11.7`；Flutter ABI 拆包对应产品 build 11178。
- SHA-256：`4033873dbf5a72086345224f2bb2f337ed39b741d9759eb58fce099889d063c4`。
- [公开源码标签](https://github.com/Maqiaogongmin/yours-app/tree/v1.11.7-public-source.2)。
- [官网 Android 下载](https://yours-app.uk/downloads/android)。

建议覆盖安装，保留本地训练数据。

[完整 Android 发布验收记录](https://github.com/Maqiaogongmin/yours-app/blob/main/docs/releases/android-1.11.7%2B11178.md)。
