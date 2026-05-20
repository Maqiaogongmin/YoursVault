# 有思 Yours

**你的训练，你的数据。**

有思是一个本地优先、数据自主的训练记录 App。前身是开源健身项目 [wger](https://github.com/wger-project/flutter)，经彻底重写后独立发展。设计灵感部分来自 [Obsidian](https://obsidian.md) 的 Vault——数据应当跟着人走，不应被锁在任何服务端。

## 核心功能

- **训练计划**：自由编排训练日和动作组，训练计时模式下完整记录训练过程。
- **动作库**：内置少量常用动作，支持自定义添加任何运动形式。
- **Yours Vault**：所有数据以开放文件夹形式保存在本地（JSON 文件）。即使 App 不再维护，数据仍可被 AI 或任何工具读取。
- **Agent 可读写**：App 保持开放性但不内嵌 AI。你可以让自己的 AI Agent 分析训练数据、生成新计划、批量修改记录——数据始终留在本地。

```
你在有思里训练 → SQLite 保存 → 导出到 Yours Vault → AI Agent 读取分析 → 生成新计划放入 inbox → 有思导入
```

## 安装包

| 文件 | 平台 | 架构 | 大小 |
|------|------|------|------|
| `Yours-arm64-v8a-1.11.0.apk` | Android | arm64-v8a | 21 MB |
| `Yours-armeabi-v7a-1.11.0.apk` | Android | armeabi-v7a | 19 MB |
| `Yours.ipa` | iOS | — | 8.3 MB |

> iOS 版本目前为未签名 IPA，需要通过自签方式安装。

## Agent Skills

`skills/` 目录包含供 AI Agent 使用的技能文件，用于通过 Yours Vault 和 Yours CLI 与有思 App 交互：

| Skill | 用途 |
|-------|------|
| `yours-vault` | 理解和操作 Yours Vault 开放文件夹协议 |
| `yours-cli` | 验证优先的 CLI 工作流（导出、检查、试运行、导入） |
| `yours-plan-author` | 生成可读的训练计划及配套 `.plan.json` 导入文件 |

Agent 通过 Vault 的 `inbox/` 目录提交文件，经过验证后导入 App。Markdown 给人看，JSON 给 App 导入，各司其职。

## 设计原则

- App 数据库归 App 内部管理，Agent 不直接操作
- Agent 通过 Yours Vault 中的可审阅文件协作
- 验证与试运行先于导入
- 数据始终由用户掌握，不依赖任何服务端

## 致谢

向 [wger](https://github.com/wger-project) 项目致敬，它是这一切的起点。感谢 [Obsidian](https://obsidian.md) 带来的 Vault 灵感——让数据跟随人走，而非受困于平台。

---

> 源码将在稳定后开源。如有想法或反馈，欢迎通过 GitHub 联系。
