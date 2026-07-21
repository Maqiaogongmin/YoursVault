# 有思 1.11.5 Android build 11163

本次发布将 arm64-v8a Android APK 对齐到当前 1.11.5 主线。

## 更新内容

- 训练计时页会根据计划目标预填重量、次数、休息、时长和备注。
- Yours Vault 支持从选定文件夹导入 inbox，并可自动发现默认 inbox。
- 继续保留备份包、公共 Documents 导出、多语言和自托管服务器同步。
- 覆盖安装旧版时保留本地训练数据和已有配置。

## 验收状态

- API 36 arm64-v8a Android 模拟器：安装、冷启动、后台恢复、二次冷启动和主导航验收通过。
- Redmi M2007J3SC Android 16 真机：保留数据覆盖安装、冷启动、后台恢复、二次冷启动、首页、训练计划、动作库、用户页和数据管理 / Yours Vault 验收通过。
- 未发现 Java、Flutter 或 native fatal 日志。

## APK

- 大多数 Android 手机：`Yours-android-arm64-v8a-1.11.5+11163.apk`
- SHA-256：`4bc756b9113e607fd42ed506d4a4793a8ccb64eb2740b3a7c95fe680d6a4e8d9`

请优先覆盖安装，不要先卸载旧版，以免被 Android 系统删除本地数据。
