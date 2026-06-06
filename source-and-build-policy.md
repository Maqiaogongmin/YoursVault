# 有思源码与构建来源规则

## 当前开源边界

有思 App 已正式上架 App Store，当前暂不开放完整源代码。

GitHub 仓库只用于公开发布以下内容：

- Android APK 安装包。
- 版本更新说明。
- 安装说明。
- 隐私政策。
- 训练免责声明。
- 官网或 App Store 跳转说明。

不要上传 Flutter / iOS / Android 工程源码、签名文件、构建脚本中的本地配置、开发者个人数据、未清理历史文件。

## 唯一构建来源

以后所有对外发布的有思安装包，都必须只从以下目录构建：

`/Users/ly/Desktop/yours-flutter/yours-app`

## 不再使用的来源

不要再从以下来源构建发布包：

- 临时 port 文件夹。
- 旧的 wger 工程副本。
- 桌面散落的历史构建目录。
- 未确认清理状态的工程压缩包。

## 发布前必须确认

- 源码没有 wger 品牌、包名、图标、文案或历史发布残留。
- 源码没有开发者个人训练计划和训练记录。
- 版本号与发布说明一致。
- Android release APK 保持在约 20 MB 量级，略超可接受。
- Android APK 使用稳定 release 签名。
- iOS archive 来自同一份源码。
- GitHub 公开发布包保留 arm64-v8a、armeabi-v7a、x86_64 三种 APK；三者必须来自同一份最新源码。

## 构建产物命名建议

Android：

- `Yours-android-arm64-v8a-<version>.apk`
- `Yours-android-armeabi-v7a-<version>.apk`
- `Yours-android-x86_64-<version>.apk`

iOS：

- TestFlight 不直接对外提供 IPA 下载。
- 正式版本通过 App Store 分发，内部测试版本可继续使用 TestFlight。
