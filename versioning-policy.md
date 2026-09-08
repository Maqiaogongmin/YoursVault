# 有思版本号规则

显示版本使用 `主版本.功能版本.修复版本`，构建号独立递增。

当前源码：`pubspec.yaml` 中 `version: 1.11.6+11176`。

| 平台 | 显示版本 | 构建号 |
| --- | --- | --- |
| iOS | CFBundleShortVersionString = 1.11.6 | CFBundleVersion = 11176 |
| Android arm64-v8a | versionName = 1.11.6 | versionCode = 13176 |
| HarmonyOS | versionName = 1.11.6 | versionCode = 11176 |

Android 拆分 ABI 的原生 versionCode 含架构偏移，不等于 Flutter 逻辑构建号；更新清单的 latestBuild 使用逻辑构建号 11176。以后发布应核验实际 APK 元数据与 App 的版本归一化逻辑。

- 同一平台、同一分发架构的新版构建号必须高于旧版。
- 同一显示版本重发也必须递增构建号，不能替换已发布附件。
- 构建时传入的版本可能覆盖工程静态配置；以最终安装包为准。
- 三个平台发布进度可能不同，见[发布状态](release-status.md)。
- 正式包保持稳定包名与签名，不使用 debug 包替代正式发布。
