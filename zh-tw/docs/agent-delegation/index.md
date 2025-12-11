---
layout: docs
title: "Agent 委派"
display_title: "Agent 委派"
permalink: /zh-tw/docs/agent-delegation/
nav_order: 4
lang: zh-TW
---

當你的 **Agentic Workflows** 已經建立並準備就緒，接下來就會遇到一個關鍵問題：要如何實際執行這些流程？你選擇的執行策略——從完全由本地控制，到高度自動化的非同步編排——會從根本上影響開發速度與學習成效。

本指南會涵蓋完整的執行光譜：從在本地 IDE 中維持緊密控制，到將複雜工作流程委派給多個並行運作的非同步 agents。每一種策略都有最適用的情境，而掌握這套決策框架，可以幫助你在每個情境下選擇正確的執行方式。

## 執行策略總覽

**Agentic Workflows** 可以透過三種主要策略來執行，每一種都在「控制、一致性」與「速度、生產力」之間做出不同平衡：

1. **本地 IDE 執行** —— 在你的開發環境內直接執行工作流程，獲得最高程度的掌控與學習
2. **非同步 Agent 委派** —— 將完整工作流程交給 GitHub Coding Agents，藉由並行作業放大生產力
3. **混合編排** —— 將本地控制與非同步委派「有策略地組合」，同時保留上下文與監督能力

關鍵洞見在於：**同一個 Agentic Workflow** 可以依照「當前需求、工作流程成熟度、對 agent 偏差的容忍度」採用不同的執行策略。

## Agentic Workflow 執行示例

為了說明這些執行策略，接下來用一個完整的 **Agentic Workflow** 作為例子：實作 OAuth 驗證功能。此工作流程會把你所有的 Agent Primitives 編排成一個系統化流程，並且可以用以下任一種策略來執行。

**範例 Workflow：** `implement-oauth-feature.prompt.md`

### Workflow 元件如何運作：

1. **Mode Activation（模式啟動）** → 啟用具備安全導向 MCP 工具邊界的 `backend-dev.chatmode.md`  
2. **Context Loading（上下文載入）** → 載入 `[auth patterns](./auth.memory.md)` 與 `[security standards](./security.context.md)`  
3. **Specification Generation（規格產生）** → 使用具備驗證標準的 `oauth-feature.spec.md` 模板  
4. **Implementation Execution（實作執行）** → 由 `security.instructions.md` 引導，並透過 `applyTo: "auth/**"` 模式自動作用  
5. **Learning Integration（學習整合）** → 將成功模式與發現的 edge cases 更新到 `.memory.md`

**關鍵洞見：** 這個 workflow 無論是在本地為了學習而執行，或是為了速度而非同步委派，都可以產生一致的結果。也就是說，「執行策略」變成與「workflow 設計」獨立的決策層。

接下來，我們會看看如何為你的具體情境，選擇並執行最適合的策略。

## A. 執行策略選擇

當你已經建立一個 Agentic Workflow，下一個問題就是「要怎麼跑它」。在本地控制與非同步委派之間做選擇，會深刻影響開發速度、風險控制與你從過程中能學到多少東西。

**✅ 快速操作：**
- **本地 IDE 執行：** 針對學習、探索新模式或高風險任務，維持最高程度控制
- **非同步 Agent 委派：** 對規格清楚、偏差風險低的任務，透過 [GitHub Coding Agent](https://docs.github.com/en/copilot/how-tos/agents/copilot-coding-agent) 最大化產出
- **混合編排：** 在保持監督與上下文的前提下，聰明地混用本地與非同步模式

> 💡 **「控制 vs. 生產力」決策框架：** 根據你對控制的需求、workflow 的成熟度，以及對 agent 偏差的容忍度來挑選策略。越重視控制 → 越偏向本地執行；越追求 throughput → 越偏向非同步委派。

### 🔧 策略決策矩陣：

```
控制偏好 → 建議策略：
├── 高度需要控制 → 本地 IDE 執行（學習、迭代、引導）
├── 以生產力為優先 → 非同步 Agent 委派（委派並監控）  
└── 追求平衡 → 混合編排（委派 + 主動監督）
```

### 快速決策指南：如何選擇執行策略

| 情境 | 本地 IDE | 非同步委派 | 混合編排 |
|------|:--------:|:----------:|:--------:|
| **第一次使用這個 workflow** | ✅ | ❌ | ✅ |
| **已非常成熟的 workflow** | ❌ | ✅ | ❌ |
| **高風險／關鍵功能** | ✅ | ❌ | ✅ |
| **需要速度／並行工作** | ❌ | ✅ | ✅ |
| **希望深入學習與理解** | ✅ | ❌ | ✅ |
| **對錯誤容忍度極低** | ✅ | ❌ | ✅ |

**⚠️ 檢查點：** 你的策略選擇必須同時對齊「控制偏好」與「agent primitives 的成熟度」。

**📊 成功指標：** 在「生產力」與「品質／控制」之間取得適當平衡。

你選擇的執行策略，不只決定開發速度，也決定你從每次實作中累積多少學習，以及整個過程中你保留多少監督與決策權。

## B. 本地 IDE 執行

如果你的目標是「最大控制與最大學習」，最適合的方式就是直接在你的開發環境內執行 Agentic Workflows。這在你探索新的 patterns、處理複雜需求，或是要深入理解實作路徑時特別重要。

**✅ 快速操作：**
- **直接執行 prompt：** 在 VS Code Chat 中使用 `/workflow-name` 來執行對應的 `.prompt.md` 檔案
- **逐步掌控流程：** 讓 workflow 分階段進行，你在每個階段都可以插手調整
- **即時學習：** 觀察 AI 在複雜決策點上的行為並適時修正

> 💡 **學習優化：** 本地執行保留了最完整的上下文，能讓你同時看到「成功模式」與「失敗模式」，特別適合作為累積專業與優化 workflow 的主要方式。

### 🔧 實作模式：

```markdown
## 本地 IDE 中執行 Agentic Workflow

1. **選擇要執行的 workflow** → 選取 `<workflow-name>.prompt.md`
2. **準備上下文** → 確保相關檔案與 specification 都在正確位置
3. **啟動執行** → 在 VS Code Chat 中使用 `/workflow-name` 觸發 workflow
4. **互動式引導** → 在驗證關卡與重要決策點給出指示
5. **學習與記錄** → 將心得記錄下來，並據此優化 workflow
```

### 本地執行的優勢

- **完全掌控：** 你可以親自確認每個決策與每一個產出
- **深度理解：** 你能看見 AI 為何做某些選擇，而不只是結果
- **即時優化：** 可以在同一個 session 內迅速調整 instructions 或 prompts
- **上下文完整保留：** 工作過程中所有決策與脈絡都在你眼前

**⚠️ 檢查點：** 本地執行以犧牲速度與 throughput 為代價，換來最大化的學習與掌控。

**📊 成功指標：** 高品質的實作結果 + 對 workflow 運作方式有深刻理解。

## C. 非同步 Agent 委派

當你想要「放大產出、提升並行能力」，而且對既有 workflow 具備足夠信心時，就可以把完整的 Agentic Workflows 委派給 GitHub Coding Agents。這個策略最適用於：workflow 已成熟、需求規格明確、偏差風險低的情境。

你的 Agentic Workflows 可以透過多種非同步委派模式來執行，從單一 agent 到多 agent 並行協作。

### C.1. 單一 Agent 委派

**✅ 快速操作：**
- **VS Code 內建：** 在 Ask 模式中使用 [`#copilotCodingAgent`](https://github.blog/changelog/2025-07-14-start-and-track-github-copilot-coding-agent-sessions-from-visual-studio-code/)，即可直接委派工作（需安裝 [GitHub Pull Requests VSCode extension](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)）
- **GitHub MCP Server：** 從任一 MCP host application 呼叫 `create_issue` 與 `assign_copilot_to_issue` 這兩個 [GitHub MCP Server tools](https://github.com/github/github-mcp-server?tab=readme-ov-file#tools)
- **GitHub Web／行動版：** 透過 [Agents 控制平面](https://github.com/copilot/agents) 直接建立任務並指派

**🔧 實作模式：**

```markdown
## 單一 Agent 的 Workflow 委派

1. **先完成 Spec 審核** → 由人類審核 `.spec.md` 規格
2. **選擇進入點**：
   - VS Code：在 Ask 視窗輸入「#copilotCodingAgent，請依照這份 spec 實作 OAuth 功能」
   - MCP：使用 `create_issue` + `assign_copilot_to_issue`，並在 body 中附上 spec
   - GitHub：由人類透過 Agents 頁面建立工作並附上 spec
3. **交付確認** → 與使用者確認將由 agent 負責後續實作
```

### C.2. 多 Agent 並行委派（Spec-to-Issues 模式）

**✅ 快速操作：**
- **Spec 拆解：** 把大型 specification 拆分成彼此獨立、不互相覆蓋的 component issues
- **Issue 產生：** 使用 GitHub MCP Server 的 `create_issue` 工具，系統化地產生多個 issue
- **平行指派：** 使用 `assign_copilot_to_issue` 將不同 issue 指派給多個 GitHub Coding Agents 並行處理

> 💡 **平行編排：** 大型 specification 可以被拆解為獨立、可平行處理的工作流，同時透過共用的架構與 context 來維持整體一致性。

**🔧 實作模式：**

```markdown
## Agentic Workflow：從單一 Spec 到多 Issue 的委派

### Phase 1：Specification 拆解
1. **元件分析** → 找出可獨立實作、彼此不重疊的元件
2. **依賴關係映射** → 定義元件之間的整合點與先後順序
3. **上下文分配** → 確保每個元件都指向共用的架構與決策文件
4. **實作依賴排序** → 用子 Issue 或標籤標明實作順序

### Phase 2：平行 Issue 產生
使用 GitHub MCP Server 工具：
- `create_issue(title: "OAuth Middleware Component", body: spec_section_1)`
- `create_issue(title: "Token Service Component", body: spec_section_2)`  
- `create_issue(title: "User Sync Service Component", body: spec_section_3)`

### Phase 3：平行 Agent 指派
- `assign_copilot_to_issue(issue_1)` → Agent A 負責 middleware
- `assign_copilot_to_issue(issue_2)` → Agent B 負責 token service
- `assign_copilot_to_issue(issue_3)` → Agent C 負責 user sync

### Phase 4：協同整合
- **進度監控** → 透過 GitHub Agents 控制平面追蹤所有 agent 狀態
- **整合測試** → 驗證跨元件互動是否符合預期
- **衝突處理** → 解決 PR 之間的衝突與重疊變更
```

### 範例：OAuth 系統拆解

```markdown
# Parent Spec：OAuth 2.0 Authentication System

## 適合平行委派的元件拆分：

### Issue 1：OAuth Middleware (`oauth-middleware`)
**範圍：** Request 攔截、provider routing、錯誤處理
**依賴：** 無（可獨立元件）
**Agent 焦點：** Middleware patterns、HTTP 處理

### Issue 2：Token Service (`token-service`)  
**範圍：** JWT 產生、驗證與 refresh 流程
**依賴：** 無（可獨立元件）
**Agent 焦點：** 密碼學操作、token lifecycle

### Issue 3：User Profile Sync (`user-sync-service`)
**範圍：** OAuth callback 處理、使用者資料同步
**依賴：** Token Service（用來識別使用者）
**Agent 焦點：** 資料轉換與持久化

### 整合時共用的 context 參考：
- 架構模式： [Auth system design](./auth.memory.md#oauth-architecture)
- API 慣例： [REST standards](./api-sec.context.md#api-design)
- 安全需求： [OAuth security checklist](./security.instructions.md#oauth)
```

**⚠️ 檢查點：** 每個元件都可以獨立實作，且具備清楚的整合契約。

**📊 成功指標：** 多個 agents 並行完成工作，而不產生範圍重疊或整合失敗。

非同步委派帶來新挑戰：如何維持品質，以及如何把 agent 的新發現回饋回你的 primitives。你需要一套有系統的方法來驗證它們的輸出，並把學習整合回 instructions 與 memory。

## D. 進度監控與非同步整合

一旦 agents 開始非同步工作，「可見度」與「可控性」就變得關鍵。本節會介紹維持監督與從非同步執行中萃取學習的關鍵做法。

### D.1. 多通道進度追蹤

**✅ 快速操作：**
- **VS Code 整合：** 透過 GitHub PR extension 的「Copilot on My Behalf」區塊監看非同步任務
- **GitHub 控制平面：** 使用 Agents 頁面集中檢視所有 agent 任務狀態

**🔧 監控能力：**

```
跨通道的進度可見性：
├── VSCode GitHub PR Extension：
│   ├── 即時 agent 狀態指示
│   ├── Draft PR 預覽與進度紀錄
│   └── 可直接檢視 agent session
└── GitHub Agents Page：
    ├── 多 agent 編排儀表板  
    ├── 跨 repository 的任務狀態
    └── Agent 效能與成功率指標
```

### D.2. 非同步 Agent 的品質關卡

**✅ 快速操作：**
1. **Draft PR 審查：** 系統性地檢視 agent 所提交的 Draft PR
2. **整合測試：** 驗證 parallel work 之間的互動是否正確
3. **上下文同步：** 把 agent 的新發現更新回你的本地知識庫

> 💡 **品質控制策略：** 把非同步 agent 的產出視為「高品質初稿」，而非「最終成品」——保留必要的人工審查，可以在維持品質的同時享受自動化帶來的速度。

**🔧 品質控制流程：**

```markdown
## 非同步 Agent 輸出整合流程

### Phase 1：Draft PR 分析
1. **Code Review** → 對 agent 的實作進行完整程式碼審查
2. **架構一致性** → 確認是否符合原始 specification
3. **安全審查** → 檢查是否遵守安全 best practices
4. **測試涵蓋率** → 確認已具備足夠的 unit／integration tests

### Phase 2：整合驗證  
1. **元件介面測試** → 驗證平行元件之間的介面是否吻合
2. **端到端測試** → 從使用者流程角度檢查完整功能
3. **效能檢查** → 確保沒有嚴重效能回歸
4. **文件檢查** → 確認有足夠的文件說明

### Phase 3：知識整合
1. **Memory 更新** → 將成功模式記錄到 `.memory.md`
2. **Instructions 強化** → 根據新的洞見改進 `.instructions.md`
3. **Template 優化** → 把驗證過的 patterns 加回 `.spec.md` 模板
```

### 範例：OAuth 整合的品質關卡

```markdown
## 非同步 Agent 輸出審查：OAuth Components

### Component 1：OAuth Middleware（Agent A）
- [x] 程式碼符合既有 middleware patterns
- [x] 錯誤處理完整
- [x] 安全檢查實作到位
- [x] Unit tests > 90% coverage
- [ ] **Issue：** 缺少 CSRF 防護 → 需在本地補上

### Component 2：Token Service（Agent B）  
- [x] JWT 操作安全
- [x] Refresh 流程正確
- [x] 錯誤處理完整
- [x] Integration tests 完整
- [x] **加分：** 發現更好的 token rotation pattern

### Component 3：User Sync Service（Agent C）
- [x] OAuth callback 處理穩健
- [x] 使用者資料轉換安全
- [x] 資料庫操作有效率
- [ ] **Issue：** 並發請求下有 race condition → 需在本地修正

### 整合後的行動：
1. **本地修正：** 處理 CSRF 與 race condition 問題
2. **知識沉澱：** 將 token rotation 改進記錄到 `auth.memory.md`
3. **流程強化：** 把 CSRF 與併發檢查加入 OAuth 規格模板
```

**⚠️ 檢查點：** 所有非同步輸出都必須通過品質關卡後，才可以完成整合。

**📊 成功指標：** 非同步 agent 所產生的變更不會導致生產事故。

## E. 混合編排策略

最成熟、也最靈活的方法，是透過「有策略的 context 管理」，把本地控制與非同步委派結合起來。這種混合策略可以在執行複雜 Agentic Workflows 時，同時保有兩種世界的優勢。

*你可以把這部分視為：在前面介紹的基本委派模式之上，專門為複雜多元件 workflow 設計的進階版本。*

**✅ 快速操作：**
- **Session 邊界清楚：** 把規劃、委派與整合拆成不同 session
- **Context 接力：** 在 sync／async 之間移交工作時，確保關鍵上下文被完整保留
- **Memory 保持：** 使用 `.memory.md` 把非同步階段的成果寫回，使之成為下次工作的起點

> 💡 **混合 context 策略：** 把非同步委派視為「帶著完整 context 的接力」而不是「context 斷裂」，這樣你就能在 agents 工作期間繼續本地開發，並在整合時自然接回前後脈絡。

### 範例：以 context 最佳化的混合工作階段

```markdown
## Session 1：規劃與委派設定
### Context Loading
- Review [project requirements](./requirements.md)
- 載入 [既有 auth patterns](./auth.memory.md)
- 產生 OAuth specification，並拆解成數個元件

### Delegation Handoff
- 透過 GitHub MCP Server 建立 3 個平行 issues
- 為每個元件指派 GitHub Coding Agents
- 在 [delegation.memory.md](./delegation.memory.md#oauth-parallel) 中記錄委派脈絡

## Session 2：本地開發（與非同步並行）
### 本地工作的新 context
- 持續開發不依賴 OAuth 的前端元件
- 透過 VS Code GitHub PR extension 監看非同步進度
- 回應 agents 針對整合提出的問題

## Session 3：整合與學習（非同步完成後）
### Context 組裝
- 檢視 agents 所送出的 draft PR
- 載入 [delegation.memory.md](./delegation.memory.md#oauth-parallel) 中的委派資訊
- 進行整合測試與 conflict 解決

### 知識累積
- 更新 [auth.memory.md](./auth.memory.md)，加入新的成功模式
- 依據學到的東西加強 [.github/instructions/security.instructions.md](./.github/instructions/security.instructions.md)
- 優化未來大型功能的委派與拆解模式
```

**⚠️ 檢查點：** 清楚的 context 交接，使得 sync／async 混合執行不會造成認知負擔。

**📊 成功指標：** 在本地與非同步工作之間切換時，不會迷失脈絡或重複工作。

## 重點整理

1. **執行策略的選擇** 是「控制 vs. 生產力」的平衡，取決於 workflow 成熟度與具體情境
2. **本地 IDE 執行** 適用於學習、探索與高風險任務，最大化理解與掌控
3. **非同步 Agent 委派** 適用於已成熟、規格明確的 workflow，藉由平行化大幅提升產能
4. **混合編排策略** 在 context 管理得當的前提下，可以同時享有本地與非同步的優點
5. **品質關卡與知識整合** 是非同步策略成功的關鍵，確保 agent 產出既安全又能反哺 primitives

**準備好擴展到團隊層級了嗎？** 接著閱讀 [團隊與企業規模](../team-adoption/)，了解如何從個人實踐擴展到團隊協調，並透過 spec-driven workflows 與企業級治理來管理這些 Agent Primitives。

**想直接看實作範本？** 可以前往 [範例](../examples/)，取得可直接使用的 primitives 組合。

你現在已經擁有完整的 workflow 執行與委派策略。下一步，就是把這些模式推廣到整個團隊與組織，使其成為日常開發不可或缺的一部分。
