---
layout: docs
title: "快速開始"
display_title: "快速開始"
permalink: /zh-tw/docs/getting-started/
nav_order: 3
lang: zh-TW
---
現在你已經了解了[三層框架](../concepts/)，是時候建立你的第一個 Agent Primitives 了。這個實作練習會立刻帶來生產力的提升，同時為更進階的工作流程打好基礎。

整體設定遵循一個合理的推進順序：先從引導 AI 行為的 instructions 開始，接著加入創造安全邊界的 chat modes，為常見任務建立可重用的 prompts，最後建立把規劃和實作銜接起來的 specification 模板。

## Instructions 架構

Instructions 是可靠 AI 行為的基石：它們是引導 Agent 的持久規則，不會塞滿你每一輪對話的即時上下文。與其在每次對話中重複相同的指導，instructions 會把你團隊的知識直接嵌入 AI 的推理過程。

關鍵洞見是「模組化」：不要只用一個巨大、到處都套用的指令檔，而是建立在特定技術或檔案類型下才會啟動的目標檔案。這種 context engineering 的做法可以讓 AI 保持專注，也讓指導內容維持高度相關。

**✅ 快速操作：**
- 在 `.github` 資料夾中為這個 repository 建立通用的 [`copilot-instructions.md`](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file) 檔案，放入共用規則
- 在 `.github/instructions/` 資料夾中，依領域（frontend、backend、testing、docs、specs...）建立模組化的 [`.instructions.md` 檔案](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files)
- 使用 [`applyTo: "**/*.{js,ts...}"`](https://code.visualstudio.com/docs/copilot/copilot-customization#_instructions-file-structure) 這類模式做選擇性套用
- 編譯成 [AGENTS.md 標準](https://agents.md)，讓你的上下文可以在所有 coding agents 上運作。想了解 **context compilation**，請見 [工具生態](../tooling/)

> 💡 **Context Engineering 實戰：** 模組化 instructions 只會在處理特定檔案類型時載入相關指南，保留更多上下文空間給程式碼理解。

### 🔧 工具與檔案：

```
.github/
├── copilot-instructions.md          # 全域 repository 規則
└── instructions/
  ├── frontend.instructions.md     # applyTo: "**/*.{jsx,tsx,css}"
  ├── backend.instructions.md      # applyTo: "**/*.{py,go,java}"
  └── testing.instructions.md      # applyTo: "**/test/**"

# 編譯 context 之後：
# 巢狀的 AGENTS.md 檔案會自動生成在最佳位置
```

### 範例：Instructions 內的 Markdown Prompt Engineering

建立 `.github/instructions/frontend.instructions.md` 檔案：

```markdown
---
applyTo: "**/*.{ts,tsx}"
description: "結合 context engineering 的 TypeScript 開發指南"
---
# TypeScript 開發指南

## Context Loading
開始前請查看 [專案慣例](../docs/conventions.md) 與
[型別定義](../types/index.ts)。

## 確定性要求
- 使用嚴格的 TypeScript 設定
- 為 React components 實作 error boundaries
- 一致地套用 ESLint TypeScript 規則

## 結構化輸出
請產生具備以下條件的程式碼：
- [ ] 所有 public API 皆有 JSDoc 註解
- [ ] 在 `__tests__/` 目錄下有對應的 unit tests
- [ ] 適當的 index 檔案中有型別匯出
```

**⚠️ 檢查點：** Instructions 已經模組化、目標清楚，並準備好被編譯。

## Chat Modes 設定

有了 instructions 架構之後，你還需要一個機制來強制執行領域邊界，避免 AI agents 超出其專業範圍。Chat modes 透過建立類似現實世界「執照」的專業邊界來達成這點——architect 負責規劃但不施工，engineer 負責實作但不決定策略。

**✅ 快速操作：**
- 定義領域特定的[自訂 chat modes](https://code.visualstudio.com/docs/copilot/chat/chat-modes)，並為其設好 MCP 工具邊界
- 在每個模式中封裝對應技術棧的知識與指南
- 為每個 chat mode 指定最合適的 [LLM 模型](https://code.visualstudio.com/docs/copilot/chat/chat-modes#_chat-mode-file-example)，例如 `Claude Sonnet 4`
- 設定安全的 [MCP 工具存取](https://code.visualstudio.com/docs/copilot/chat/chat-modes#_chat-mode-file-example)，避免跨領域的安全問題

> 💡 **透過 MCP 工具邊界實現安全：** 每個 chat mode 只拿到它領域真正需要的 MCP 工具——避免危險的權限升級與交叉污染。就像專業執照一樣，planning mode 不能執行破壞性指令，frontend mode 不能直接碰 backend 資料庫。

### 🔧 工具與檔案：

```
.github/
└── chatmodes/
  ├── architect.chatmode.md             # 規劃專家——只設計、不執行
  ├── frontend-engineer.chatmode.md     # UI 專家——只做介面、不能碰 backend
  ├── backend-engineer.chatmode.md      # API 專家——只做服務、不改 UI
  └── technical-writer.chatmode.md      # 文件專家——只寫文件、不跑程式碼
```

### 範例：MCP 工具邊界實作

建立 `.github/chatmodes/backend-engineer.chatmode.md` 檔案：

```yaml
---
description: '專注於安全的後端開發專家'
tools: ['changes', 'codebase', 'editFiles', 'runCommands', 'runTasks', 
    'search', 'problems', 'testFailure', 'terminalLastCommand']
model: Claude Sonnet 4
---

你是一位專注於安全 API 開發、資料庫設計與伺服器端架構的後端開發專家。你優先考慮 security-first 的設計模式與完整的測試策略。

## Domain Expertise
- RESTful API 設計與實作
- 資料庫 schema 設計與最佳化
- Authentication 與 authorization 系統
- 伺服器安全與效能優化

你完全掌握本專案的後端，因為你已閱讀所有 [backend 文件](../../docs/backend)。

## Tool Boundaries
- **可以**：修改後端程式碼、執行 server 指令、跑 tests
- **不可以**：修改 client-side assets
```

### 安全與專業邊界

- **Architect mode**：只有 research 工具——**不能執行破壞性指令或修改 production code**
- **Frontend Engineer mode**：只有 UI 開發工具——**不能存取資料庫或 backend services**
- **Backend Engineer mode**：只有 API 和資料庫工具——**不能修改前端介面或資產**
- **Technical Writer mode**：只有文件相關工具——**不能跑程式碼、部署或存取敏感系統**

就像現實世界的專業執照一樣，每個模式都只在自己的專業範圍內運作，不能跨界做危險的事。

**⚠️ 檢查點：** 每個 mode 都有清楚的邊界與工具限制。

## Agentic Workflows

Chat modes 建立了安全邊界，但你仍然需要有效的方式來執行完整的開發流程。**Agentic Workflows** 以可重用的 `.prompt.md` 檔案形式存在，將所有 primitives 編排成系統化、端到端的流程。

**✅ 快速操作：**
- 建立[`.prompt.md` 檔案](https://code.visualstudio.com/docs/copilot/copilot-customization#_prompt-files-experimental)來代表完整的開發流程
- 在流程中設計「必經」的人類驗證關卡
- 設計同時支援本地執行與非同步委派的工作流程

> 💡 **Agentic Workflows：** 這些 `.prompt.md` 檔案是你的「完整系統化流程」，把所有 primitives（instructions、modes、specs、context）組合起來，變成可以在本地或委派執行的可重複工作流程。

### 🔧 工具與檔案：

```
.github/prompts/
├── code-review.prompt.md           # 內建驗證關卡
├── feature-spec.prompt.md          # 以 spec-first 方法論為中心
└── async-implementation.prompt.md  # 用來委派給 GitHub Coding Agent
```

### 範例：完整的 Agentic Workflow

建立 `.github/prompts/feature-spec.prompt.md` 檔案：

```markdown
---
mode: agent
model: gpt-4
tools: ['file-search', 'semantic-search', 'github']
description: '帶有驗證關卡的功能實作工作流程'
---
# Feature Implementation from Specification

## Context Loading Phase
1. Review [project specification](${specFile})
2. Analyze [existing codebase patterns](./src/patterns/)
3. Check [API documentation](./docs/api.md)

## Deterministic Execution
Use semantic search to find similar implementations
Use file search to locate test patterns: `**/*.test.{js,ts}`

## Structured Output Requirements
Create implementation with:
- [ ] Feature code in appropriate module
- [ ] Comprehensive unit tests (>90% coverage)
- [ ] Integration tests for API endpoints
- [ ] Documentation updates

## Human Validation Gate
🚨 **STOP**: Review implementation plan before proceeding to code generation.
Confirm: Architecture alignment, test strategy, and breaking change impact.
```

**⚠️ 檢查點：** Prompts 中已明確定義驗證關卡。

## Specification Templates

最後一塊基礎是處理「規劃到實作」中間的落差。Specification 模板會把高階想法轉化為「實作就緒」的藍圖，不論是人還是 AI agent 都能依此產生一致的結果。

這些 `.spec.md` 模板是 **spec-driven team workflows** 的基礎。當你擴展到團隊情境時（參見 [Team & Enterprise Scale](../team-adoption/)），產品負責人在 sprint 規劃時會用這些模板，建立明確、可由 agent 執行的 specifications。[Spec-Kit](https://github.com/github/spec-kit) 提供 `/speckit.specify` 指令，可以依照「constitution → specify → plan → tasks → implement」這套模式產生這些檔案；理解模板結構則讓你能為團隊客製化。

**✅ 快速操作：**
- 建立標準化的 [`.spec.md` 模板](https://docs.github.com/en/copilot/copilot-chat/copilot-chat-cookbook) 來撰寫功能規格
- 把驗證條件（validation criteria）寫入規格，使其「實作就緒」
- 讓規格設計成在「規劃」與「實作」之間有明確交接的文件

> 💡 **橋樑 Primitive：** Specification 檔會把規劃階段的思考，轉化為可由人或 AI 穩定執行的實作藍圖。

### 🔧 工具與檔案：

```
.github/specs/
├── feature-template.spec.md        # 標準功能規格模板
├── api-endpoint.spec.md           # API 專用規格模板
└── component.spec.md              # UI component 規格模板
```

### 範例：實作就緒的 Specification

建立 `.github/specs/jwt-auth.spec.md` 檔案：

```markdown
# Feature: User Authentication System

## Problem Statement
Users need secure access to the application with JWT-based authentication.

## Approach
Implement middleware-based authentication with token validation and refresh capabilities.

## Implementation Requirements
### Core Components
- [ ] JWT middleware (`src/middleware/auth.ts`)
- [ ] Token service (`src/services/token.ts`)
- [ ] User validation (`src/services/user.ts`)

### API Contracts
- `POST /auth/login` - Returns JWT token
- `POST /auth/refresh` - Refreshes expired token
- `GET /auth/verify` - Validates current token

### Validation Criteria
- [ ] Handles malformed tokens with 401 status
- [ ] Token expiration properly managed
- [ ] Refresh token rotation implemented
- [ ] Unit tests >90% coverage
- [ ] Integration tests for all endpoints

## Handoff Checklist
- [ ] Architecture approved by team lead
- [ ] Database schema finalized
- [ ] Security review completed
- [ ] Implementation ready for assignment
```

**⚠️ 檢查點：** Specifications 在委派前就已經達到「實作就緒」。

## 快速開始清單

當上述 primitives 都建立好之後，你就擁有一套完整的基礎，可以開始打造系統化的 AI 開發流程。以下清單說明推薦的實作順序，最終目標是建立完整的 Agentic Workflows。

### 概念基礎
1. **[ ]** 理解 **Markdown Prompt Engineering** 原則（語義結構 + 精確性 + 工具）
2. **[ ]** 掌握 **Context Engineering** 基礎（context window 最佳化 + 會話策略）

### 實作步驟  
4. **[ ]** 建立 [`.github/copilot-instructions.md`](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file)，寫入專案基本指南（Context Engineering：global rules）
5. **[ ]** 設置具 `applyTo` 模式的領域特定 [`.instructions.md` 檔](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files)（Context Engineering：selective loading）
6. **[ ]** 編譯 instructions 成 `AGENTS.md` 標準，讓 context 可在不同 agents 間通用——詳見 [工具生態](../tooling/)
7. **[ ]** 針對你的技術棧設定[自訂 chat modes](https://code.visualstudio.com/docs/copilot/copilot-customization#_custom-chat-modes)（Context Engineering：domain boundaries）
8. **[ ]** 建立第一個 [`.prompt.md` Agentic Workflow](https://code.visualstudio.com/docs/copilot/copilot-customization#_prompt-files-experimental)
9. **[ ]** 為功能規格打造第一個 `.spec.md` 模板（Agent Primitive：從規劃到實作的確定性橋樑）
10. **[ ]** 以「規格先行」方式練習兩個 Agentic Workflows（會話分割）：先規劃、再實作

## 下一步？

**基礎都完成了嗎？** 你已經建立第一批 Agent Primitives，也理解它們如何運作。在進入執行策略之前，建議先閱讀 [工具生態](../tooling/)，了解讓這些 primitives 可以擴展的基礎設施——context compilation、套件管理，以及支撐所有這些能力的 Agent CLI runtimes。

**想再多理解理論嗎？** 可以回到 [核心概念](../concepts/) 深入閱讀。

**已經迫不及待想往下走？** 在 Tooling 之後，[Agent 委派](../agent-delegation/) 會介紹執行策略，而 [團隊與企業規模](../team-adoption/) 則說明如何在組織層級導入這套方法。

你現在已經擁有完整的 Agent Primitives，以及第一個 Agentic Workflow。下一步，就是理解背後的基礎設施，讓這些 primitives 真正做到可執行、可分享、可上線。
