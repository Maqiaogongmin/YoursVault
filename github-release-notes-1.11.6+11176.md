# 有思 1.11.6 Android build 11176

本次发布将 Android 版对齐到 iOS 1.11.6 主线，重点调整训练计时和训练记录的备注逻辑。

## 更新内容

- 计划动作备注会显示在计时输入中作为参考，但未编辑时不会自动写入训练记录。
- 用户填写的每组备注会独立保存；切换到下一组时不会误带入。
- 已完成训练组的备注可以直接继续编辑，无需重新保存整组数据。
- 练后备注与每组备注保持独立，并可在训练记录页分别查看和修改。
- 补齐备注草稿、训练记录、数据库迁移与同步快照测试。

## 验收状态

- Flutter 静态分析通过，完整测试 180 项通过。
- arm64-v8a APK 的 `versionName=1.11.6`、`versionCode=13176`，APK Signature Scheme v2 验证通过。
- Pixel 8 / Android 16 模拟器完成覆盖安装、训练计时、备注新增与二次编辑、训练结束、记录展示、后台恢复和第二次冷启动验收。
- Android 真机测试已由发布负责人确认通过。
- 未发现 Flutter 或 Android fatal 日志。

## APK

- 大多数 Android 手机：`Yours-android-arm64-v8a-1.11.6+11176.apk`
- SHA-256：`b5f571c049da00cca7098ef0cc3fc8fde6b39e17a9d7318d6d5aa170ebece8e2`
- 对应公开源码 tag：`v1.11.6-public-source.1`

请优先覆盖安装，不要先卸载旧版，以免被 Android 系统删除本地数据。
