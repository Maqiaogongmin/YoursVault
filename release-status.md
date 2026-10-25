# 有思发布状态与下载验证

状态记录：2026-10-25。商店审核状态可能变化，请以实际状态为准。

| 平台 | 本次版本 | 状态 |
| --- | --- | --- |
| Android | 1.11.7+11178 | 已发布至官网和 GitHub Releases，arm64-v8a |
| HarmonyOS | 1.11.7 (11178) | 正式签名包已成功提交华为应用市场审核；查询在架版仍为 1.11.6 (11176) |
| iOS | 本次不调整 | Android／鸿蒙已同步到 iOS 1.11.7 共享业务代码；实际版本以 App Store 为准 |

## 下载与校验

- [官网下载](https://yours-app.uk/downloads/android)
- [GitHub 发布包、源码和 SHA256SUMS](https://github.com/Maqiaogongmin/YoursVault/releases/tag/v1.11.7%2B11178)
- [App 更新清单](https://yours-app.uk/latest.json)
- APK：`Yours-android-arm64-v8a-1.11.7+11178.apk`，28,087,220 字节。
- SHA-256：`4033873dbf5a72086345224f2bb2f337ed39b741d9759eb58fce099889d063c4`。

官网回下载文件已核对与 GitHub 发布包一致。APK 的 Android versionCode=13178，对应 Flutter arm64 ABI 拆包后的产品 build 11178；更新清单使用产品 build，与 App 现有归一化逻辑一致。

## 本次更新与验证

- 修复重复同名动作记录覆盖，持久化替换动作的参数和动作快照。
- 同步备份、服务器同步的动作身份、训练快照和训练记录标题显示。
- Flutter 静态分析通过，182 项测试通过。
- Android 16／Pixel 8／arm64 模拟器覆盖安装、冷启动、四个主页面、训练记录、Vault 导入导出和后台恢复通过；导出结果确认两个卧推分别保留 40 kg 和 55 kg。
- 鸿蒙 Pura 90／HarmonyOS 6.1.1 模拟器使用正式 APP 内的签名 HAP 安装，完成启动、四个主页面、计划编辑、训练保存、冷启动和后台恢复。
- 两端均确认：替换后的深蹲 70 kg、6 次、休息 30 秒在冷启动后保留。鸿蒙记录页显示对应值。
- 本次未做 Android／鸿蒙真机验证。鸿蒙有框架／模拟器非致命日志，未观察到崩溃或记录失败。

## 源码与华为提交

- [公开源码标签 v1.11.7-public-source.2](https://github.com/Maqiaogongmin/yours-app/tree/v1.11.7-public-source.2)
- [Android 发布验收记录](https://github.com/Maqiaogongmin/yours-app/blob/main/docs/releases/android-1.11.7%2B11178.md)
- 141 个 lib/assets 文件与构建工作区一致；源码 .2 修正旧鸿蒙版本断言，业务代码不变。
- 鸿蒙 APP SHA-256：`00a9e337b20fb000cff6d8e9ea84084a5bf405257c115079733c73d0d02fcc7b`。
- AGC 包 ID：`2068983789152913920`。提交返回 ret.code=0，随后查询 versionCode=11178、releaseState=12；这不代表审核通过或已上架。
- zh-CN、en-US、ja-JP 更新说明已写入并回读核对。
- 未配置 `.bugly_env`，未上传 Bugly 符号表；堆栈还原需要另行配置。
