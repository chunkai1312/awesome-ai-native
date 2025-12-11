---
layout: docs
title: "參考資料"
display_title: "參考資料"
permalink: /zh-tw/docs/reference/
nav_order: 7
lang: zh-TW
---

這裡整理了 AI Native Development 在長期實作與精進過程中所需的關鍵清單、進程框架與文件參考。

## 快速開始清單

### 概念基礎
1. **[ ]** 理解 **Markdown Prompt Engineering** 原則（語義結構 + 精確度 + 工具）
2. **[ ]** 掌握 **Context Engineering** 基礎（buffer／context window 最佳化 + 會話策略）

### 實作步驟
3. **[ ]** 建立包含基本專案指南的 [`.github/copilot-instructions.md`](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file)（Context Engineering：全域規則）
4. **[ ]** 設置具有 `applyTo` pattern 的領域特定 [`.instructions.md` 檔案](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files)（Context Engineering：選擇性載入）
5. **[ ]** 為你的技術棧領域配置 [chat modes](https://code.visualstudio.com/docs/copilot/copilot-customization#_custom-chat-modes)（Context Engineering：領域邊界）
6. **[ ]** 建立第一個具備驗證 checkpoint 的 [`.prompt.md` 檔案](https://code.visualstudio.com/docs/copilot/copilot-customization#_prompt-files-experimental)（Markdown Prompt Engineering：確定性模板）
7. **[ ]** 為功能規格建立第一個 `.spec.md` 模板（Agent Primitive：從規劃到實作的確定性橋樑）
8. **[ ]** 練習 spec-first 工作流程：先規劃、後實作（Context Engineering：會話分割）
9. **[ ]** 使用 [GitHub Coding Agent](https://docs.github.com/en/copilot/about-github-copilot/about-copilot-coding-agent) 嘗試一次非同步委派（進階 orchestration）
10. **[ ]** 建立團隊層級的治理與驗證關卡（Human-AI 協作模式）

## 精通進程

### Foundation Level（基礎階段）

**目標：** 理解核心概念並建立第一批 primitives  
**時間投入：** 約 2–3 小時  
**關鍵成果：**
- [ ] 建立基本的 `.instructions.md` 檔案
- [ ] 配置第一個 chat mode
- [ ] 建立第一個 `.prompt.md` 模板
- [ ] 對整體理論框架有初步掌握

**下一步：** 進入 Beginner 階段，開始實際運用。

### Beginner Level（初級階段）  

**目標：** 讓基本 instructions 與 prompts 持續、穩定地發揮作用  
**時間投入：** 約 4–6 小時  
**關鍵成果：**
- [ ] 有運作中的領域特定 instructions
- [ ] 已配置多個 chat modes
- [ ] 建立含 3–5 個模板的 prompt library
- [ ] 在日常開發中體驗到較為一致的 AI 行為

**下一步：** 進入 Intermediate 階段，導入 workflow pattern。

### Intermediate Level（中級階段）

**目標：** 建立具備 context 最佳化的 spec-driven 工作流程  
**時間投入：** 約 8–12 小時  
**關鍵成果：**
- [ ] 以 spec-first 為主的規劃方法論
- [ ] 實作多種 Context Engineering 策略
- [ ] 能針對複雜任務進行會話分割
- [ ] 逐步採用 Memory-driven 開發模式

**下一步：** 進入 Advanced 階段，導入非同步委派。

### Advanced Level（高級階段）

**目標：** 掌握非同步委派與多 Agent 編排  
**時間投入：** 約 15–20 小時  
**關鍵成果：**
- [ ] 能運用 GitHub Coding Agent 進行任務委派
- [ ] 建立並行多 agent 的工作流程
- [ ] 具備完善的品質關卡與驗證流程
- [ ] 已實作混合型（Hybrid） context 策略

**下一步：** 進入 Expert 階段，擴展到團隊與組織層級。

### Expert Level（專家階段）

**目標：** 建立團隊規模的治理機制與前沿 pattern 創新  
**時間投入：** 約 25+ 小時  
**關鍵成果：**
- [ ] 建立團隊規模的協調框架（如 spec-driven sprints）
- [ ] 建構知識分享與 primitives 共用系統
- [ ] 將治理、合規與安全需求整合進 instructions 與 workflows
- [ ] 針對 AI Native Development 提出並實驗新的 pattern

**下一步：** 持續為社群知識與前沿實務貢獻案例與工具。

## 範式轉移

*傳統思維：「告訴 AI 要做什麼」*  
**Agent Mastery 思維：「為最佳認知效能設計 context 與結構」**

### 核心原則

1. **透過結構追求確定性：** 以系統化方式設計 prompts 與 workflows，讓結果更可預測
2. **Context 即效能：** 把記憶與上下文視為「效能資源」，而不只是附屬品
3. **複合智慧：** 系統應該能透過迭代與學習持續進化，而不只是一組固定規則
4. **人機夥伴關係：** 透過驗證關卡與協作流程，結合人類判斷與 AI 速度
5. **團隊規模協調：** 把知識、規則與 workflows 分享給整個組織，而不是只存在個人腦中

### 關鍵洞見

- **你需要的確定性越高，就越需要強調 Markdown Prompt Engineering 與更小、更明確的任務範圍**
- **專案越複雜，Context Engineering 就越是關鍵的成功因素**
- **同時掌握這兩者，你在 agent 驅動開發中的穩定性與品質會出現「質變」**

**記住：** 從小處開始、快速迭代，然後再透過這些前沿概念的系統化應用來穩定擴張。

## 文件參考

### 社群資源

- **[Awesome GitHub Copilot](https://github.com/github/awesome-copilot)** —— 社群維護的清單，彙整了各種 instructions、prompts 與 chat modes，涵蓋主流語言與框架

### VS Code Copilot 自訂

- **[主要自訂指南](https://code.visualstudio.com/docs/copilot/copilot-customization)** —— VS Code Copilot primitives 的完整總覽
- **[全域 Instructions（.github/copilot-instructions.md）](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilot-instructionsmd-file)** —— 針對整個 workspace 的統一指令
- **[模組化 Instructions（.instructions.md）](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-instructionsmd-files)** —— 具 `applyTo` pattern 的領域特定 instructions
- **[Prompt Files（.prompt.md）](https://code.visualstudio.com/docs/copilot/copilot-customization#_prompt-files-experimental)** —— 可重用的任務導向 prompts
- **[Custom Chat Modes](https://code.visualstudio.com/docs/copilot/copilot-customization#_custom-chat-modes)** —— 自訂 domain-specific chat behavior

### GitHub Copilot 官方文件

- **[GitHub Copilot Overview](https://docs.github.com/en/copilot)** —— 完整的 GitHub Copilot 官方文件
- **[GitHub Coding Agent](https://docs.github.com/en/copilot/about-github-copilot/about-copilot-coding-agent)** —— 針對 issue 與 PR 的非同步 agent
- **[Enabling Coding Agent](https://docs.github.com/en/copilot/how-tos/agents/coding-agent/enabling-copilot-coding-agent)** —— 啟用與設定流程
- **[MCP Integration](https://docs.github.com/en/copilot/how-tos/agents/coding-agent/extending-copilot-coding-agent-with-the-model-context-protocol-mcp)** —— 擴充 agent 能力的 MCP 整合
- **[Copilot Chat Cookbook](https://docs.github.com/en/copilot/copilot-chat/copilot-chat-cookbook)** —— 各種有效 prompting 的實例
- **[Responsible Use Guidelines](https://docs.github.com/en/copilot/responsible-use-of-github-copilot-features/responsible-use-of-copilot-coding-agent-on-githubcom)** —— 在 GitHub.com 使用 Coding Agent 的負責任使用準則

## 快速疑難排解

### 常見問題與對應解法

**問題：** AI 回應品質與風格不一致  
**解法：** 將 prompts 強化為結構化 Markdown，清楚標出目標、步驟與驗證關卡

**問題：** Context window 不足或經常「忘記」先前資訊  
**解法：** 採用 session splitting 與具 `applyTo` 的模組化 instructions，避免一次塞入過多上下文

**問題：** 團隊在使用 AI 時協調成本過高  
**解法：** 建立共享 primitive library 與 repository 級別的協作規範

**問題：** 非同步 agents 產出品質參差不齊  
**解法：** 在 workflows 中內建品質關卡，並將 agent 輸出視為需要人工審查的「草稿」而非最終成品

**問題：** 對合規與安全風險有疑慮  
**解法：** 實作風險分級的 agent 邊界，並在 instructions 中明確嵌入政策條款

## 成功指標追蹤

### 個人層級指標

- **Productivity（生產力）：** 每個功能或任務平均耗時的降低幅度
- **Quality（品質）：** 缺陷數量與返工次數的減少
- **Consistency（一致性）：** AI 輸出風格與結構的一致程度
- **Learning（學習）：** 對新技巧與 primitives 的採用速度

### 團隊層級指標

- **Coordination（協調）：** merge conflict、溝通成本與等待時間的降低
- **Knowledge Sharing（知識分享）：** primitives 在成員間的重用率
- **Onboarding（新人成長）：** 新成員達到穩定產能所需時間
- **Innovation（創新）：** 團隊內獨創 AI Native pattern 的量與質

### 組織層級指標

- **Adoption（採用程度）：** 使用 AI Native Development 實務的團隊比例
- **Compliance（合規）：** 對治理與政策框架的遵循程度
- **ROI（投資報酬）：** AI 工具引入後在生產力與品質上的綜合改善
- **Innovation Frontier（創新前沿）：** 組織在 AI Native 發展上的領先程度與外部影響力

## 下一步

### 本週可以做的事（Immediate Actions）

1. 完成上方的 [快速開始清單](#快速開始清單) 中對你最關鍵的幾項
2. 從主指南的首頁（`../`）選擇一條最適合你的學習路徑
3. 實際建立並使用第一個 Agent Primitive

### 這個月可以推進的事（Short Term）

1. 為你的主要 domain 建立一套完整的 primitives library
2. 練習與調整 1–2 個核心 workflows（如 code review、spec-first 實作）
3. 與團隊成員分享實作成果與學到的模式

### 下個季度可以規劃的事（Medium Term）

1. 建立團隊層級的協調與治理流程
2. 將 AI Native Development 納入正式的工程準則
3. 建立並持續追蹤成功指標，定期檢討

### 今年可以完成的事（Long Term）

1. 達到 Expert 級別的實務水準
2. 積極對外分享經驗與模式，回饋社群
3. 推動整個組織向 AI Native 轉型

*這份參考指南是你在 AI Native Development 旅程中的常備工具。當你需要快速查詢、評估進度或尋找下一步行動時，可以隨時回到這裡。*
