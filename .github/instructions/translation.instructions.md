---
applyTo: "zh-tw/**/*.md"
description: "繁體中文翻譯指引 - 規範術語處理與翻譯風格"
---

# 繁體中文翻譯指引

## 術語處理原則

### 保留英文原文的術語
以下術語應保留英文原文，首次出現時可加註中文說明：

**核心 Agent Primitives：**
- Agent Primitives（代理原語）
- Instructions Files
- Chat Modes
- Prompt Files
- Agentic Workflows
- Specification Files (.spec.md)
- Memory Files (.memory.md)
- Context Files (.context.md)

**技術概念：**
- Markdown Prompt Engineering
- Context Engineering
- Context Window
- MCP (Model Context Protocol)
- AGENTS.md
- applyTo 模式

**工具與平台：**
- GitHub Copilot
- VS Code / VSCode
- APM (Agent Package Manager)
- Spec-Kit
- GitHub Coding Agent

### 翻譯的術語
以下術語應翻譯為中文：

| 英文 | 繁體中文 |
|------|----------|
| Layer | 層 |
| Framework | 框架 |
| Validation Gates | 驗證關卡 |
| Workflow | 工作流程 |
| Knowledge Sharing | 知識分享 |
| Team Coordination | 團隊協調 |
| Governance | 治理 |
| Compliance | 合規 |
| Best Practices | 最佳實踐 |

## 翻譯風格指南

### 語氣
- 使用專業但平易近人的語氣
- 避免過度正式或口語化
- 保持技術準確性

### 格式
- 保留原文的 Markdown 結構
- 保留程式碼區塊中的英文
- 保留檔案路徑和命令的英文

### 標點符號
- 使用全形標點符號（，。！？：；）
- 英文術語與中文之間不需加空格（但可視情況調整以提升可讀性）

### 範例格式
首次出現術語時：
```
Agent Primitives（代理原語）是 AI Native Development 的核心概念...
```

後續使用：
```
透過 Agent Primitives，你可以建立可重用的 AI 工作流程...
```

## Front Matter 格式

所有 zh-tw 文件必須包含：
```yaml
---
layout: docs
title: "[中文標題]"
display_title: "[中文顯示標題]"
permalink: /zh-tw/docs/[section]/
nav_order: [數字]
lang: zh-TW
---
```

## 連結處理

內部連結應指向 zh-tw 版本：
```markdown
# 正確
[核心概念](../concepts/)
[快速開始](../getting-started/)

# 避免
[Core Concepts](/docs/concepts/)
```

## 品質檢查清單

翻譯完成後請確認：
- [ ] 所有保留英文的術語使用正確
- [ ] Front matter 包含 `lang: zh-TW`
- [ ] 內部連結指向正確的 zh-tw 路徑
- [ ] 程式碼區塊保持英文
- [ ] 標點符號使用全形
- [ ] 整體語句通順自然
