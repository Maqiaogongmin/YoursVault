# 有思发布状态与下载验证

状态记录：2026-09-08。商店审核状态可能随后变化，请以商店页面为准。

| 平台 | 本次版本 | 状态与分发 |
| --- | --- | --- |
| Android | 1.11.6+11176 | 已发布；官网经 Cloudflare 分发，GitHub Releases 保留原始发布包 |
| iOS | 1.11.6 (11176) | 2026-09-07 已提交 App Store 审核；提交时在售版为 1.11.5 |
| HarmonyOS | 1.11.6 (11176) | 2026-09-08 已提交 AppGallery 审核；提交后查询在售版仍为 1.11.5 (11174) |

## Android 下载与校验

- [官网下载](https://yours-app.uk/downloads/android)
- [GitHub 版本与 SHA256SUMS](https://github.com/Maqiaogongmin/YoursVault/releases/tag/v1.11.6%2B11176)
- [App 更新清单](https://yours-app.uk/latest.json)
- 最新发布包：`Yours-android-arm64-v8a-1.11.6+11176.apk`，28,087,220 字节。
- SHA-256：`b5f571c049da00cca7098ef0cc3fc8fde6b39e17a9d7318d6d5aa170ebece8e2`。

官网下载文件与 GitHub 发布包已核对一致。历史版本中的其他 ABI 包不代表当前版本；当前 1.11.6 发布提供 arm64-v8a。

官网迁移到 Cloudflare 分发后，已补回 App 使用的 `/latest.json`，其中下载地址指向 `/downloads/android`。以后调整网站部署时应同时检查这两个公开入口。

## 源码与验收记录

主 App [公开源码](https://github.com/Maqiaogongmin/yours-app)版本为 `1.11.6+11176`，已有冻结标签 `v1.11.6-public-source.1`。

本次维护对比了公开仓库与发布工作区已有的 `lib/`、`assets/`、`test/`、`ohos/` 文件：差异为测试示例路径脱敏及配置空白。鸿蒙使用同一 Flutter 业务代码和 `ohos/` 工程，通过 Flutter-OH 单独构建；不能仅根据壳层静态版本字段推断最终安装包版本。

鸿蒙 11176 已在 Pura 90 模拟器进行启动、训练记录、训练组备注与练后备注编辑、后台恢复、冷启动后数据保留检查。此记录不代表全部功能或鸿蒙真机验收。签名包已提交商店；商店审核通过不应由本仓库的版本号推断。
