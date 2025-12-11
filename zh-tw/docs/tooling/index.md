---
layout: docs
title: "工具生態"
display_title: "工具生態：擴展 Agent Primitives"
permalink: /zh-tw/docs/tooling/
nav_order: 3
lang: zh-TW
---

你已經掌握了[三層框架](../concepts/)，也理解你的 Agent Primitives 是**用自然語言編寫的可執行軟體**。接下來很自然會問：這些 markdown 檔案，要怎麼從「你個人在 VS Code 裏的開發」擴展到「生產等級的基礎設施」？

答案其實和每一個程式語言生態系走過的路很像。就像 JavaScript 一開始只是瀏覽器腳本，後來發展出 Node.js runtime、套件管理器與部署工具一樣，你的 Agent Primitives 也需要一整層對應的基礎設施，才能真正發揮威力。

## 自然語言即程式碼

你的 Agent Primitives 具備專業軟體的典型特徵：模組化、可重用性、依賴關係、版本管理，以及持續演進。這不只是比喻——這些 `.prompt.md` 與 `.instructions.md` 檔案代表了一種新的「軟體」形式，需要對應級別的工具與基礎設施來支援。

當你的 Agent Primitives 逐漸成熟時，會發生什麼事？

- **模組化**：將關注點拆分到不同 primitives 檔案，彼此協同運作
- **可重用性**：同一組 primitives 可以在不同專案與上下文中可靠運作  
- **依賴關係**：需要管理 MCP servers、外部工具與上下文需求
- **演進**：隨著 workflow 改善持續調整與版本更新
- **發佈**：團隊希望像分享 code library 一樣分享已驗證的 primitives

從這個視角來看，你會開始用「軟體工程」而不只是「寫 prompt」的角度，來思考 AI 開發工具。也因此，你的自然語言程式同樣需要 runtime、套件管理與部署工具等完整基礎設施。

## Agent CLI Runtimes

多數開發者會在 VS Code 中透過 GitHub Copilot 來撰寫與執行 Agent Primitives——這很好，對互動式開發、除錯與日常 workflow 調整都很理想。但就像 JavaScript 最終需要 Node.js 才能跳出瀏覽器一樣，你的自然語言程式也需要 **Agent CLI Runtimes** 才能在自動化與生產情境中發揮作用。

新興生態系中，已經出現多家廠商針對這個需求提供實作，例如：**OpenAI Codex CLI**、**Anthropic Claude Code**、**Google Gemini CLI**，以及未來陸續出現的 runtimes。這些工具提供命令列介面，讓你可以在 CI/CD 或伺服器環境中執行 Agent Primitives，並使用各家模型的能力。

### Inner Loop vs Outer Loop

關鍵在於理解每一個環境最適用的時機：

- **Inner Loop（VS Code + GitHub Copilot）**：適合互動式開發、測試與 workflow 微調
- **Outer Loop（Agent CLI Runtimes）**：適用於可重現執行、CI/CD 整合與正式部署

Agent CLI Runtimes 會把你的 Agent Primitives 從「只能在 IDE 裡手動呼叫的檔案」，轉變為可以**在任何環境中穩定執行的自動化工作流程**。它們提供命令列執行、CI/CD 整合、環境一致性，以及對 MCP servers 的原生支援——也就是把你的日常開發成果橋接到實際的生產環境。

## Runtime 管理

VS Code + GitHub Copilot 已經足以支援個人層級的開發，但團隊要的是**共享、版本管理，以及產品化**這些 Agent Primitives。當你同時面對多個 CLI 環境時，很快就會碰上安裝流程不同、設定方式不一、相容性組合爆炸等問題。

[Agent Package Manager](https://github.com/danielmeppiel/apm)（APM）透過提供「統一的 runtime 管理與 agent package 發佈」來解決這件事。你不再需要手動安裝與設定每一家廠商的 CLI——APM 幫你處理複雜度，同時保留你在 VS Code 裡已經熟悉的工作流程。

實際上，runtime 管理大概長這樣：

```bash
# 安裝 APM（一次即可）
curl -sSL https://raw.githubusercontent.com/danielmeppiel/apm/main/install.sh | sh

#（選用）設定 GitHub PAT，以使用 GitHub Copilot CLI
export GITHUB_COPILOT_PAT=your_token_here

# 交給 APM 幫你安裝 runtimes
apm runtime setup copilot        # 安裝 GitHub Copilot CLI（推薦）
apm runtime setup codex          # 安裝 OpenAI Codex CLIs

# 檢查目前有哪些 runtimes
apm runtime list                 # 顯示已安裝的 runtimes
apm runtime status               # 顯示實際會被使用的是哪一個

# 安裝 MCP 依賴（類似 npm install）
# 注意：此功能仍在開發中
apm install

# 將 Instructions 檔案編譯成 Agents.md 檔
apm compile

# 透過指定 runtime 執行 workflow
# 這會觸發類似下列指令：
# 'copilot --log-level all --log-dir copilot-logs --allow-all-tools -p  security-review.prompt.md'
# 具體行為可參考下方範例 apm.yml
apm run copilot-sec-review --param pr_id=123 
```

這樣一來，幾個關鍵好處會立刻浮現：

- 你在 VS Code 裏的日常開發流程 **完全不用改**
- APM 自動幫你安裝與設定各家 runtimes
- 不論實際底層用哪個 runtime，你的 workflows 一律可以執行
- 同一個 `apm run` 指令，可以在不同 runtime 組合下保持一致行為

**✅ 檢查點：** Runtime 的複雜度已被抽象化掉，你只需要專注在 workflows 本身。

## Context Compilation 與最佳化

你的模組化 `.instructions.md` 檔案在 VS Code 內已經很好用，但目前仍然綁死在那個環境裡。若要在其他 coding agents（例如 Cursor、Claude Desktop 等）中重用，你需要一個通用的標準——也就是 `AGENTS.md`。當你從多個 packages 引入 primitives 時，還需要一個聰明的方式把它們合併，避免上下文互相污染。

**Compilation 可以同時解決這兩件事：**把 VS Code 專用的 instructions 轉換成可攜式的 `AGENTS.md` 檔案，並在此過程中最佳化「本地 primitives 與依賴項的 context 如何組合」。這正是讓 [Team & Enterprise Scale](../team-adoption/) 裡提到的 **spec-driven 團隊協調** 真正可行的關鍵。

[APM 的編譯器](https://github.com/danielmeppiel/apm) 會分析你的 `applyTo` pattern，對應你的目錄結構，然後產出一個最佳化的 `AGENTS.md` 階層，確保「完整覆蓋」又「最小冗餘」：

```bash
# 1. 照平常方式撰寫模組化 primitives
.apm/instructions/
├── security.instructions.md      # applyTo: "**/auth/**"
├── react.instructions.md         # applyTo: "**/*.{tsx,jsx}"
└── api-design.instructions.md    # applyTo: "backend/api/**"

# 2. 執行 compilation
apm compile

# 3. 會自動產生最佳化的 AGENTS.md 階層
├── AGENTS.md                     # Global context（最小化）
├── frontend/AGENTS.md           # React patterns
└── backend/
    ├── AGENTS.md                # Backend patterns
    └── auth/AGENTS.md           # Security + backend
```

**關鍵好處：**

- **可攜性：** 任何支援 AGENTS.md 標準的 coding agent 都能使用這些 context
- **效率：** 相較於手動管理，per-file context 量更小、更精準
- **覆蓋保證：** 能「數學上」保證每個檔案都拿到應該有的 instructions
- **維護簡單：** 只要修改 primitives，再重新 compile，AGENTS.md 就會自動更新
- **團隊協調：** 只要更新 instructions，透過 compile 結果就能快速同步到整個專案

```bash
$ apm compile --verbose

Generated 5 AGENTS.md files --- Context efficiency: 46.7%

Placement Distribution
├─ .                      Constitution and 5 instructions from 4 sources
├─ tests                  2 instructions from 3 sources
├─ docs                   1 instructions from 2 sources
├─ backend/api            2 instructions from 4 sources
└─ scripts/deployment     1 instructions from 1 source
```

對小型專案（大約 5–10 個 instruction 檔）來說，手動維護 `AGENTS.md` 仍然可行——你可以參考 [快速開始](../getting-started/)。但一旦規模超過這個範圍，或開始使用依賴 packages，編譯就變成幾乎必須的步驟。技術細節可以參考 [APM Compilation 文件](https://github.com/danielmeppiel/apm/blob/main/docs/compilation.md)。

**✅ 檢查點：** Compilation 讓 context 既可攜又最佳化，且可以跨 agents、跨專案擴展。

## 發佈與封裝

當你的 Agent Primitives 被證明有價值時，你自然會想要：

1. **在團隊內分享**  
2. **在更多專案中重用**  
3. **最終放到生產環境使用**

這正是與傳統軟體開發最類似的地方——你需要套件管理、依賴解析、版本控制與發佈機制。

問題很快會浮現：你已經打造了強大的 Agent Primitives，團隊也想用，但單靠「丟一堆 markdown 檔案」來傳遞很快就失控，更不要說不同環境下的 MCP 依賴與設定檔管理。

[APM](https://github.com/danielmeppiel/apm) 提供類似 npm 的「自然語言程式套件管理」：你可以建立可發佈的 packages，具備依賴、版本與組合能力。這也是 [Team & Enterprise Scale](../team-adoption/) 裡所說的 **agent onboarding 與 enterprise governance** 的底層基礎。

### 套件管理實務

```bash
# 建立一個 APM 套件
apm init security-review-workflow

# 撰寫 .apm/instructions/*.instructions.md 等檔案

# 在本地開發與測試 workflow
cd security-review-workflow 
apm compile && apm install
apm run copilot-sec-review --param pr_id=123

# 把 APM package 發佈到 GitHub：
git tag v1.0.0 && git push --tags
```

APM 專案會有一個 `apm.yml` 設定檔，角色類似於 `package.json`，用來定義 scripts、dependencies 與輸入參數等：

```yaml
# 讓團隊成員可以安裝並使用你的 primitives
# 專案根目錄的 apm.yml（類似 package.json）
name: security-review-workflow
version: 1.2.0
description: Comprehensive security review process with GitHub integration
scripts:
  copilot-sec-review: "copilot --log-level all --log-dir copilot-logs --allow-all-tools -p  security-review.prompt.md"
  codex-sec-review: "codex security-review.prompt.md"
  codex-debug: "RUST_LOG=debug codex security-review.prompt.md"
  
dependencies:
  apm:
    - company/compliance-rules
    - company/design-guidelines
  mcp:
    - github/github-mcp-server
```

當你進行 context compilation 時，多個 APM packages 可以同時針對相同的 `applyTo` pattern 發揮作用而不互相衝突。舉例來說：當 `company/compliance-rules`、`company/design-guidelines` 與本地專案都鎖定 `**/auth/**`，compile 會把三方 context 合併起來，並附上來源 attribution——形成一個疊加式、可組合的 context。

**真實範例：** 專案 [corporate-website](https://github.com/danielmeppiel/corporate-website) 依賴了 `compliance-rules` 與 `design-guidelines`。在執行 `apm install && apm compile` 之後，compliance pattern 會自動套用在 data handling code 上、design standards 套用在 frontend components 上，並與本地 context 組合在一起——零衝突，完整覆蓋。

**企業治理模式：** 當合規團隊更新 `company/compliance-rules` 中的資料保存政策，全公司每個團隊只要執行一次 `apm install && apm compile`，所有 projects 中的 agents 都會立刻遵守新的政策。這就是**可驗證的 agent onboarding at scale**——政策不再只是培訓文件，而是實際可執行的 primitives。

這些好處會快速疊加：

- 用版本化套件發佈已驗證的 workflows 與 instructions
- 自動安裝所需 MCP servers 與其他依賴
- 追蹤 workflow 的演進並維持相容性
- 從社群 primitives library 中汲取既有設計
- 保證不同團隊成員之間的執行結果一致
- 為企業級政策更新與治理提供立即生效的機制

**✅ 檢查點：** 你的 Agent Primitives 現在已經是具備依賴管理與版本控制的可發佈軟體單元。

## 生產環境部署

工具生態的最後一塊，就是讓你能在生產環境中建立 **Continuous AI**——也就是在 CI/CD pipelines 中自動執行封裝好的 Agent Primitives。你在開發過程中打造的 workflows，現在可以用與傳統軟體同樣可靠的方式自動跑在各種環境。

以前面的 `security-review-workflow` package 為例，以下展示如何透過多 runtime 策略在 CI 中部署：

```yaml
# .github/workflows/security-review.yml
name: AI Security Review Pipeline
on: 
  pull_request:
    types: [opened, synchronize]

jobs:
  security-analysis:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        script: [codex-sec-review, copilot-sec-review, codex-debug]  # 對應 apm.yml 中的 scripts
    permissions:
      models: read
      pull-requests: write
      contents: read
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Run Security Review (${{ matrix.script }})
      uses: danielmeppiel/action-apm-cli@v1
      with:
        script: ${{ matrix.script }}
        parameters: |
          {
            "pr_id": "${{ github.event.number }}"
          }
      env:
        GITHUB_COPILOT_PAT: ${{ secrets.GITHUB_COPILOT_PAT }}
      
```

**關鍵連結：** `matrix.script` 的值（`codex-sec-review`、`copilot-sec-review`、`codex-debug`）與 `apm.yml` 中 scripts 欄位完全對應。[APM](https://github.com/danielmeppiel/apm) 會自動安裝所需 MCP 依賴（例如 `ghcr.io/github/github-mcp-server`、`security-scanner-mcp`），並把 `pr_id` 參數傳給你的 `security-review.prompt.md` workflow。

這樣一來，你可以建立兼具：

- **runtime 彈性**：同一個 workflow 可以在不同 runtime 組合上跑
- **平行執行**：透過 matrix 策略並行跑多個 agents 或模式
- **環境一致性**：無論在哪個 repo 或專案，部署行為保持一致
- **品質流程**：將 AI workflow 納入標準 CI/CD pipeline 中

**✅ 檢查點：** 你的 Agent Primitives 現在可以在生產環境中自動、穩定地執行，與其他軟體部署流程並列。

## 生態系演進

整個 tooling 生態的演化，其實遵循著所有成功程式語言生態系的共同路徑。理解這個模式，可以幫助你預測 AI Native Development 的走向，也能更好地定位你現在在做的事。

演進大致分成四個階段：

1. **Raw Code** → Agent Primitives（`.prompt.md`、`.instructions.md` 檔案）
2. **Runtime Environments** → Agent CLI Runtimes（Codex CLI、Claude Code 等）
3. **Package Management** → [APM](https://github.com/danielmeppiel/apm)（發佈與編排層）
4. **Thriving Ecosystem** → 共享函式庫、工具與社群 packages

就像 npm 透過解決「套件發佈」問題讓 JavaScript 生態爆發一樣，[APM](https://github.com/danielmeppiel/apm) 透過提供缺少的基礎設施層，讓「分享與擴展自然語言程式」變得實際可行，進而催生整個 Agent Primitive 生態系。

## 重點總結

1. **自然語言即程式碼** —— 你的 Agent Primitives 是真正的軟體，值得擁有完備的工具與基礎設施
2. **Agent CLI Runtimes** 讓這些 primitives 可以在 VS Code 之外執行，特別是在 CI/CD 與生產情境中  
3. **Runtime 管理** 透過 APM 把多家 vendor 的 Agentic Coding 環境抽象化，並保留 VS Code 內的開發體驗
4. **Context Compilation** 把模組化 `.instructions.md` 轉譯成可攜又最佳化的 `AGENTS.md` 階層
5. **套件管理與發佈** 讓 Agent Primitives 可以像 npm 套件那樣被版本化、分享與組合
6. **生產環境部署** 讓這些 primitives 成為現代軟體交付流程中的一等公民

**準備好開始執行 workflows 了嗎？** 現在你已經有生產等級的基礎設施，可以前往 [Agent 委派](../agent-delegation/) 學習從本地 IDE 控制到高階非同步編排的各種執行策略。

**想直接看更進階的執行模式？** 可以同樣前往 [Agent 委派](../agent-delegation/)，了解如何運用這一整套 tooling 來同時協調多個本地與非同步 agents。
