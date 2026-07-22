# 有思 1.11.5+11174

## Android arm64-v8a

- 修复公共 Documents/有思/YoursVault 目录初始化，首次导出会同时创建 inbox。
- “导入 inbox”会直接读取已授权的默认目录，不再重复打开文件管理器。
- 修复 Vault 导入完成后的错误误报，以及 MediaStore 重复导出生成 `manifest (1).json` 的问题。
- 拆分 Android 平台桥接和高复杂度 Flutter 模块，补齐关键单元测试与真机验收脚本。
- 已通过 Redmi Android 真机覆盖安装、Yours Vault 导入归档、重复导入、后台恢复和致命日志验收。
