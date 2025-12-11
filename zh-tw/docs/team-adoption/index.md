---
layout: docs
title: "團隊與企業規模"
display_title: "團隊與企業規模"
permalink: /zh-tw/docs/team-adoption/
nav_order: 5
lang: zh-TW
---

在協調團隊與維持企業治理的同時，保留 AI 帶來的生產力提升。

你已經作為個人開發者精通了 AI Native Development —— 你的 `.prompt.md` 工作流程能處理完整的功能，你的非同步 agents 整夜工作，你的生產力實實在在提升了 10 倍。但當你把這套做法帶進你的五人 Scrum 團隊時，事情開始出問題。每日站會變成匯報各個 agent 進度的狀態會；Sprint 規劃被切割成「誰要把什麼東西委派給哪一個 agent」。協調成本開始吞噬你原本的所有生產力紅利。

企業使用者的問題揮之不去：*「AI 生產力到底要怎麼擴展到傳統的團隊結構？」*

大多數團隊忽略了一個關鍵洞見：**你不需要激進重組，你需要的是讓協調變得明確的 spec-driven 工作流程。** 讓你個人高效的那些 primitives，會成為讓整個團隊一起高效的協調機制。而且關鍵是，這些相同的 primitives，亦同時支撐起比傳統方法更強韌的企業治理能力。

本節會從「個人精通」一路銜接到「團隊協調」，說明 Agent Primitives 如何從單人開發擴展到整個組織，同時維持——甚至提升——治理與合規標準。

## 團隊協調挑戰

當你第一次體驗到 AI Native Development 帶來的生產力爆發時，那感覺幾乎像魔法。你從寫臨時 prompt，進化到建立系統化的 primitives；從手動寫程式碼，進化到把整個功能委派給非同步 agents。你的個人開發速度提升了 10 倍。

接著，你試著把這套做法擴展到你的團隊。

突然之間，你 Scrum 團隊裡的五位開發者都同時在對 agents 進行委派。合併衝突倍增。兩個開發者在不知情的情況下，把有重疊的工作指派給他們各自的 agents。那些在你單獨作業時引導你的部落知識——該碰哪些元件、該遵循哪些模式、該處理哪些邊界情境——既不會傳遞給 agents，也不會傳遞給隊友。Sprint 規劃變成一場協調惡夢：「如果你的 agent 能在星期三前完成 auth service，我的 agent 就可以開始做 user profile——前提是 Sarah 的 agent 還沒動到資料庫 schema。」

原本的生產力收益，就這樣蒸發在協調開銷裡。

**錯誤的解決方案：激進重組**

這往往是許多團隊得出「必須完全拋棄傳統結構」結論的地方。於是出現一個假設：「我們需要小型的『產品工程師』團隊，能夠端對端擁有並完全獨立交付功能。」把原本協調良好的團隊拆成數個獨立單位，消除相依關係，讓 AI 強化過的個人在各自的平行孤島裡工作。

這種作法看起來很吸引人，因為它似乎保留了個人的 AI 生產力。但是它忽略了一個基本事實：**大多數真正有價值的軟體，都需要協調。** 驗證系統會與使用者個人資料整合；金流會跟庫存管理串接；前端元件依賴後端 API。消除協調，就等於消除整合，最後產出的是一堆彼此斷裂的片段，而不是一個連貫的產品。

**真正的解決方案：Spec-Driven 協調**

真正的突破在於：**AI 生產力並不是透過隔離來擴展，而是透過明確的協調 primitives 來擴展。** 你個人已經掌握的那些 Agent Primitives，成為讓整個團隊以 AI 速度協作的共享語言。

當部落知識被寫進 `.instructions.md` 檔案時，每個開發者與每個 agent 都會繼承相同的理解。當產品需求被寫成 `.spec.md` 檔案時，每一位團隊成員都以同一份規格為依據工作。當驗證關卡被內建在工作流程裡時，agent 產出的程式碼與人類產出的程式碼，其品質得以維持一致。

協調成本不再隨著 AI 使用而上升，反而下降。因為明確的 primitives 將同步會議、Slack 對話與口頭交接，替換成非同步、可重用、可被機器理解的工件。

本節會說明：要如何在協調團隊的同時保留 AI 帶來的生產力紅利——不是透過重組，而是透過你已經掌握的 primitives 的系統化應用。

## Spec-Driven 團隊工作流程

這個協調上的突破，源自一個簡單的認知：**軟體開發一直以來就有明確的階段，而這些階段本身就是自然的協調邊界。** 你不會同時設計資料庫 schema 又寫前端畫面——你會先定義要建什麼、再規劃怎麼建、把工作拆成任務，最後才進入實作。這些階段無論你有沒有說出口，都客觀存在。

AI Native Development 的貢獻在於：透過 primitives，將這些階段「明示化」，把原本隱性的協調，變成具體的工件。[Spec-Kit](https://github.com/github/spec-kit) 將這種做法稱為「Spec-Driven Development」，並提出一個清楚的工作流程：**constitution → specify → plan → tasks → implement**。每一個階段都會產出一組作為協調機制的工件；每一個階段都與熟悉的 Agile 儀式對應；而且，每一個階段都提供了自然的治理驗證關卡。

你的 Agent Primitives，正是讓這種協調模式得以運作的構件。

### Constitution 階段：團隊基礎

每個團隊都有自己的標準，只是多數團隊是透過部落知識、很快就過時的入職文件，以及「我們一向都是這樣做的」這類說法在傳遞。Constitution 階段，就是把這些基礎透過 `.instructions.md` 檔案與 `.chatmode.md` 邊界明確寫下，並且讓它們具備「可執行性」。

這個階段通常在專案初始化時進行一次，之後每季或在標準演進時再做調整。技術主管與架構師會在這裡主導，將例如「我們使用具有一致錯誤處理的 RESTful API」、「所有元件必須有超過 90% 測試覆蓋率」、「資料庫遷移必須經過架構審查」之類的決策具體寫下。

輸出成果就是你的 `.github/copilot-instructions.md` 檔案，以及帶有 `applyTo` 模式的領域特定 `.instructions.md` 檔案。舉例來說，你的後端團隊會建立 `backend.instructions.md`，清楚定義 API 模式、錯誤處理標準與安全需求。**這件事只需要做一次。** 從那一刻起，凡是處理後端檔案的開發者與 agents，都會自動繼承這些標準。

這對團隊協調的幫助極大：新同事不需要經歷好幾週的程式碼審查才能摸清模式——agents 早就依這些標準在工作。整體一致性提升，因為標準是明文的，而不是依賴於「誰還記得在 code review 裡提起它」。

對企業治理來說，這也是「合規需求」真正落腳的地方。GDPR 資料處理規則？寫在 `gdpr-compliance.instructions.md`；安全政策？寫在 `security-standards.instructions.md`。更重要的是，這些可以透過 APM（在[工具生態](../tooling/)章節有更完整說明）被打包與分發：

```bash
apm install acme-corp/security-standards
```

每一個專案、每一個 agent，都能立即遵循標準。我們會在後面的「Agent Onboarding 與企業治理」小節再深入說明。

### Specify 階段：要建什麼

產品思維會在 Sprint 規劃或待辦清單優化時，被轉換成 `.spec.md` 規格檔。產品負責人會描述要建什麼與為什麼要建，重點放在使用者價值與商業需求，而不是技術實作細節。

在傳統團隊中，這通常發生在 refinement 會議裡：產品負責人口頭說明功能，開發者提出釐清問題，然後每個人帶著略有不同的心智模型離開。部落知識就這樣累積起來：「記得，auth token 會在 24 小時後過期。」這句話也許只在會議中被提到一次，等到三個 Sprint 之後開始實作時，早就被忘得一乾二淨。

Spec-driven 團隊會建立明確的規格。使用 Spec-Kit 時，產品負責人會執行：

```bash
/speckit.specify Build a user authentication system with email/password login, 
session management, and password reset functionality. Users should remain 
logged in for 24 hours. Security is critical - follow OWASP guidelines.
```

輸出會是 `user-auth.spec.md`：包含清楚的問題描述、實作方法、驗收標準與安全考量。這個檔案會存在於儲存庫中，與程式碼一起受版本控制。當開發者在兩週後開始實作時，他們會先讀這份 spec；當 QA 撰寫測試案例時，他們也會參考這份 spec；下次在未來的某個 Sprint 需要類似功能時，團隊只要把 spec 複製一份再做調整即可。

沒有部落知識的流失，也沒有「我記得產品負責人好像有說過會話過期時間」這種模糊印象。所有東西都變成明確、可重用、可版本化的規格。

在團隊協調上，這帶來顯著的改善：多位開發者可以讀同一份 spec，然後並行實作不同元件。這是非同步優先：理解需求不再需要會議。對 agents 來說，這些規格提供了進行精準實作所需的上下文。

### Plan 階段：怎麼建

技術架構決策在這個階段進行——資深工程師與架構師會決定該如何實作這份規格。要採用哪些技術？元件架構長什麼樣子？服務彼此如何通訊？資料庫 schema 怎麼設計？

傳統上，這些討論會發生在架構審查會議，或是幾次「快速的 Slack 討論」中，關鍵決策因此被切碎在各種訊息歷史裡。當實作真的開始時，開發者就各自帶著不同假設進場：有人預期會用 REST，有人已經開始以 GraphQL 的思路建東西；資料庫 schema 的衝突，也往往是在整合階段才被發現。

Spec-driven 團隊會把規劃過程顯性化。使用 Spec-Kit 時，技術領導會這樣做：

```bash
/speckit.plan Use JWT tokens for session management. Auth service exposes 
REST endpoints. PostgreSQL for user storage. Redis for session cache. 
Follow microservices pattern - auth service is independent.
```

輸出會是一份技術計畫，明確記錄元件拆分、技術選擇、API 合約與資料庫 schema。這份文件會成為 `.context.md` 檔，或是專門的規劃文件，用來引導後續實作。

**驗證關卡：** 在委派實作之前，架構必須先被核准。這是一個人工驗證檢查點——資深工程師或架構師會在工作開始前審查這份計畫。這不是因為我們不信任 agents，而是因為架構層面的錯誤代價極高。這個關卡可以在不犧牲 AI 生產力的前提下，維持整體品質。

團隊協調上的好處是：清晰的元件邊界使得並行工作成為可能。開發者 A 建立 auth 服務，開發者 B 建立 session cache 整合，開發者 C 更新前端——大家都依照相同的架構計畫行事。沒有衝突，也不會重工。

### Tasks 階段：Sprint 拆解

在 Sprint 規劃期間，整個團隊會一起把計畫拆解成可並行執行的工作單元。技術計畫被拆成一個個離散的任務，每一個都有清楚的驗收標準與完成條件。

這正是許多團隊在 AI 協調上卡關的地方：「既然 agents 可以實作完整功能，我們要怎麼分配工作？」——答案跟沒有 agents 的時候一樣：把工作拆成依賴最少的、可測試的獨立單元。

Spec-Kit 會自動協助完成這件事：

```bash
/speckit.tasks
```

輸出是：從計畫中產生 12 個 GitHub Issues。每一個都是隔離的，可以被分配給某一位開發者（與他所使用的 agent）。例如：
- Task 1: Create user database schema and migrations
- Task 2: Implement JWT token generation service  
- Task 3: Build password hashing utilities
- Task 4: Create login endpoint with validation
- Task 5: Implement session cache with Redis
- ...and so on

每一個任務都會包含驗收標準、連結到對應的 spec 與 plan，並且有明確的完成條件。接下來開發者就可以並行推進工作——協調模式在這裡被真正啟動。

團隊協調的改善在於：任務隔離可以避免 agents 做到彼此重疊的工作。GitHub Projects 讓依賴關係變得一目了然。開發者會領取任務，使用 `.prompt.md` 工作流程將實作委派給 agents，然後在清楚邊界下並行推進，而不會互相踩線。

### Implement 階段：開發者 + Agent 執行

這正是你在[Agent 委派](../agent-delegation/)中所學到的 `.prompt.md` 工作流程與非同步委派能力真正派上用場的地方。每位開發者會接下自己被分配的任務，然後選擇直接實作，或是委派給 agents。

使用 Spec-Kit 的情境下，可以這樣做：

```bash
/speckit.implement
```

或是透過你自訂的 `.prompt.md` 工作流程：

```bash
apm run implement-from-spec --param spec="user-auth.spec.md" --param task="4"
```

agent 會依照 spec、plan 與 constitution（也就是你的 `.instructions.md` 標準）來產出實作。測試也會一起生成。程式碼會被提交到 feature branch，並建立一個清楚標明對應任務、spec 與 plan 的 PR。

**驗證關卡：** 最終的程式碼品質，仍然透過程式碼審查來確保。合併前必須有人類審核通過。開發者會用審查人類程式碼的同一套標準來看待 agent 生成的程式碼——檢查邏輯是否正確、測試是否充分、是否符合安全考量。差別只在於：因為 agents 產出程式碼的速度更快，因此審查流程要更有效率，但品質門檻並不會因此降低。

在這個階段的團隊協調模式是：開發者在各自的任務上獨立推進；agents 在背景中夜以繼日地完成被指派的實作。隔天早上的站會變成：「我的 agent 已經完成 login endpoint 了——PR 已經準備好，你們今天可以審一下。我接下來會去 review session cache 的實作。」協調的主軸不再是同步會議，而是 PR 與 GitHub Projects。

### 協調改善的本質

Spec-driven 工作流程，會從根本上改變團隊的運作樣貌：

**Spec 寫一次，反覆被消費。** 產品負責人只需要寫一次 `user-auth.spec.md`。五位開發者會讀它，三個 agents 會用它作為實作上下文，QA 會用它當作撰寫測試案例的依據，未來的新團隊也可以在類似功能上複用這份 spec。協調成本被前置到「寫規格」這一步，之後就可以在所有「消費者」身上攤提。

**非同步優先的溝通模式。** 不再是「我們開個會，我口頭講一次需求」；開發者會直接閱讀 spec。不再是「我們當初說 session timeout 要設多少？」；大家會回頭打開 plan 文件確認。同步協調的需求大幅下降。

**明確邊界讓並行工作成為可能。** 當任務被妥善拆分，且依賴關係在 GitHub Projects 裡清楚可見，多位開發者就能同時作業而不互相干擾。agent 所產生的 PR 不會互相衝突，因為元件擁有權是明確的。

**部落知識變成被捕捉的知識。** 在完成 OAuth 實作之後，團隊會建立 `auth-patterns.instructions.md`，把這次的實作方式寫下來。未來所有的驗證相關實作都會繼承這個模式。知識不再散落在 Slack 歷史裡，而是變成能持續被複用的資產。

**驗證關卡在不微管理的前提下維持品質。** 在各個階段邊界（架構核准、程式碼審查）進行人工驗證，可以在讓 agents 有高度自主性的同時，維持整體品質。你不需要「盯著 agent 寫程式」，你只需要在自然的檢查點上驗證結果。

這就是 AI 生產力如何在團隊中擴展：不是靠切割與隔離，而是透過系統化的 primitives，讓協調變得明確、非同步且高效。

> 💡 **Spec-Kit 參考**：想實際操作這個流程嗎？[Spec-Kit](https://github.com/github/spec-kit) 提供了多個 slash 指令（`/speckit.constitution`、`/speckit.specify`、`/speckit.plan`、`/speckit.tasks`、`/speckit.implement`），可以把整個流程 scaffold 出來。我們在這裡介紹的是底層框架——說明 Agent Primitives 如何讓這些模式在不依賴特定工具的情況下運作。你可以用 Spec-Kit 來實作 spec-driven 工作流程，也可以用自己的 `.prompt.md` 檔案打造客製化自動化，或同時結合這兩種做法。

## C. 知識分享與團隊智慧模式

這樣的結果，就是「複合式智慧」：每一個 Sprint 都會讓 primitive 函式庫變得更好，使後續實作變得更快、更可靠。變聰明的不只是個別開發者，而是整個團隊。

## Agent Onboarding 與企業治理

每一家企業都有開發者的 onboarding 流程：要讀哪些文件、要學哪些程式碼標準、要完成哪些安全訓練、要理解哪些合規要求。一位新開發者，往往需要花上數週時間吸收部落知識、參加各種會議，慢慢內化「我們這裡的作法」。

當你把 coding agents 帶進團隊時，它們同樣也需要 onboarding。差別在於：**agent 的 onboarding 可以是確定性的、即時的，且透過 context 注入來強制執行。**

這會把「企業治理」從一個訓練問題，轉變成一個工程問題。而工程問題，是可以用系統方法解決的。

### Agent Onboarding：以 Context 作為即時訓練

當一位新人類開發者加入你的企業時，他會收到：
- 安全政策文件（50 頁）
- GDPR 合規訓練（4 小時的影片）  
- 無障礙指引（WCAG 2.1 標準文件）
- 程式碼風格指南（內部 wiki）
- 架構決策紀錄（Confluence）

三週之後，他開始變得有生產力。六個月之後，他大致內化了多數標準。但即使如此，他仍然可能偶爾漏掉邊界情境、忘記特定要求，或偏離既有模式——畢竟，人類記憶是有限且會遺忘的。

當一個新的 coding agent 加入你的團隊（例如某位開發者開始使用 GitHub Copilot、Cursor 或 Claude Code）時，它會收到：
- `security-policy.instructions.md`（透過 `applyTo` 模式自動載入）
- `gdpr-compliance.instructions.md`（在修改使用者資料時啟用）  
- `accessibility-standards.instructions.md`（套用在所有前端程式碼上）
- `code-style.instructions.md`（對每一個檔案生效）
- `architecture-decisions.context.md`（作為查詢用的參考資料）

零秒之後，它就已經合規。每一個決策都根據政策來做。沒有被遺忘的需求，沒有需要「逐步學習」的曲線，onboarding 是即時且確定性的。

這就是企業治理上的重大突破：**政策變成 primitives，而 primitives 是可以被強制執行的。**

### 透過 APM 分發的集中治理

當你有 50 位開發者分佈在 30 個專案上時，挑戰就來了：要怎麼確保每一個專案裡的每一個 agent 都遵守相同的企業標準？當法規改變時，又要怎麼同步更新這些政策？如果不想依賴人工稽核，要如何保證一致性？

APM 套件管理（在[工具生態](../tooling/)裡有詳細說明）提供了一個分發機制：

```yaml
# 每個專案的 apm.yml 中都會包含：
dependencies:
	apm:
		- acme-corp/security-standards
		- acme-corp/gdpr-compliance  
		- acme-corp/accessibility-rules
```

開發者在專案啟動時執行 `apm install`。企業標準會被注入為一系列 `.instructions.md` 檔案。Context 編譯（在「工具生態」章節會提到）會把這些檔案放在目錄樹中最合適的位置。之後，凡是在該專案上工作的 agents，都會自動遵守這些企業政策。

當 GDPR 規範有所變動時，合規團隊只需要更新 `acme-corp/gdpr-compliance` 套件：

```bash
# 在企業合規儲存庫裡
cd gdpr-compliance
# 更新 .apm/instructions/data-handling.instructions.md
git commit -m "Update: GDPR data retention from 5 to 7 years"
git push
```

所有專案的開發者只需要執行：

```bash
apm update
```

每個專案、每一個 agent，就會在新規範下立即合規。不需要重新訓練，不需要額外的合規說明會，也不需要手動散佈政策文件。這就是**在企業規模下進行 agent onboarding**：政策被打包成 primitives，透過 APM 分發，並在 Agent Primitives 上自動強制執行。

### 以驗證關卡作為品質保證

Spec-driven 的各個階段，天然地提供了驗證檢查點，而這些檢查點會成為治理落地的關鍵節點。

回顧前面的說明：
- **Constitution 階段** → 定義標準  
- **Specify 階段** → 需求被明確化
- **Plan 階段** → **驗證關卡：架構審查與核准**
- **Tasks 階段** → 工作被拆分與指派
- **Implement 階段** → **驗證關卡：程式碼審查**

每一個驗證關卡，都是人工檢查治理是否被滿足的地方：

**架構審查關卡** 確保設計在實作前就已符合企業標準。一位資深架構師會檢視計畫：是否遵循安全政策？是否依 GDPR 規範處理使用者資料？是否符合無障礙要求？在 agents 開始實作之前，必須先獲得核准。

**程式碼審查關卡** 則確保具體實作符合品質標準。開發者會審查 agent 所產生的 PR，檢查：是否遵循已核准的架構？安全模式是否落實？測試覆蓋是否足夠？是否達成無障礙標準？合併前必須通過人工審核。

關鍵洞見在於：**這些關卡不會拖慢 AI 帶來的生產力，反而是在不犧牲速度的前提下維持品質。** agents 會在關卡之間高速實作，人類則在邊界檢查結果。實務上，這往往比傳統做法更有效率，因為品質問題不會在開發後期才被發現，也不需要昂貴的返工。

透過**風險分級的自動化層級**，你可以調整 agents 擁有的自主程度：

- **低風險元件**（文件、測試、UI 微調）：允許 agents 全自動實作，事後再進行審查
- **中風險元件**（商業邏輯、API、資料庫變更）：允許 agents 實作，但合併前必須有人類審核  
- **高風險元件**（驗證、金流、加密）：僅允許在人類嚴密引導下使用 agent，不允許完整自動化實作

這套風險框架會在 constitution（`.instructions.md` 檔案）裡被定義，並透過上述驗證關卡強制執行。治理因此從「臨時決定」變成「系統性流程」。

### 稽核追蹤與合規可視性

企業治理需要可追蹤性：誰做了什麼決策？為什麼採用這種做法？什麼時候完成安全審查？在這點上，agent 協助開發其實比傳統開發更利於建立稽核追蹤。

**agent 的決策會被記錄** 在 PR 描述、提交訊息與文件中。因為 agents 是依據明確的 spec 與 plan 進行實作，他們的推理鏈會變得可追溯：「依 `auth-plan.md` 的架構與 `security-policy.instructions.md` 的要求，實作 JWT token 服務。」整條決策鏈因此變得顯性。

**人類的核准紀錄** 則透過 GitHub 的 review 機制被保留下來。架構審查的結果會寫在計畫文件的 review 註解中；程式碼審查的核准會以 PR 的 approval 形式記錄，包含審查者身分與時間戳。合規儀表板可以彙整這些資料。

**spec 的沿革關係** 也提供了完整可追溯性。實作對應到任務，任務對應到計畫，計畫對應到 spec，spec 則對應到產品需求。從「已部署程式碼」一路回溯到「商業價值」，每一個步驟都有文件為證。

這讓稽核追蹤在實務上變得真正有用：
- 「請列出本季所有驗證系統的實作。」→ 你可以查詢被標註為 `auth-system`、`agent-generated`、`security-approved` 的 PR。  
- 「請驗證使用者資料處理是否符合 GDPR。」→ 你可以檢查相關 PR 是否都包含引用 `gdpr-compliance.instructions.md` 的審查紀錄。

傳統開發常常依賴非正式的決策與四散的文件；而結合 spec-driven 工作流程的 agent 協助開發，則會自然產生可查詢、可組合的稽核紀錄。

### 重新想像企業治理

真正的範式轉移在於：**在 AI Native Development 的世界裡，企業治理不但沒有變弱，反而變得更強。**

傳統治理仰賴：
- 人類訓練（記憶有限、學習是漸進的）
- 手動政策執行（容易不一致）
- 定期稽核（問題被延遲發現）
- 以文件為中心的合規（政策與程式碼脫節）

AI Native 治理則仰賴：
- 以 primitives 為基礎的訓練（即時、準確、不會遺忘）
- 自動化政策執行（透過 `.instructions.md` 檔案一致落實）  
- 持續驗證（在每個階段邊界都有檢查點）
- 與程式碼緊密結合的合規（政策成為 agents 的上下文）

結果就是：**開發速度更快，但治理更強。** agents 提升實作速度，而 primitives 則確保標準被遵守。驗證關卡避免了微管理，卻維持了品質；而因為決策都被顯性記錄，稽核追蹤也變得更加完善。

對那些因治理顧慮而對 AI 協助開發有所遲疑的企業來說，這裡傳達的是相反的訊息：**AI Native Development 反而讓治理變得更系統化、更可執行，也更容易被稽核。**

## 團隊角色與 Primitive 擁有權

Spec-driven 工作流程並不會抹除團隊角色，反而讓責任更清晰。產品負責人仍然負責定義「要建什麼」；架構師仍然負責決定「要怎麼建」；開發者仍然是實際執行的人。真正的變化是：這些決策不再只是短暫存在於會議紀錄或 Slack 對話裡，而是變成可重用的 primitives。

我們用一個 Sprint 週期來看看，各個角色如何對 primitives 的建立做出貢獻，並共同累積團隊智慧。

### Sprint 週期：角色實戰

**第 0 週：產品負責人 —— 需求定義**

在 backlog refinement 期間，產品負責人提出一個新功能想法：為使用者驗證系統新增「重設密碼」功能。傳統上，這些內容會在會議裡口頭描述，最後只被簡單記錄在零散的會議紀錄中。而在這裡，他會改成建立一份明確的規格：

```bash
/speckit.specify Users need ability to reset forgotten passwords via email. 
Send reset link, verify token, allow new password entry. Security is critical - 
tokens expire after 1 hour. Must work on mobile and desktop.
```

輸出會是一份 `password-reset.spec.md`，存放在儲存庫中。這份 spec 包含問題描述、使用者價值、驗收標準與安全考量。它是版本控制的、可引用的、也可重用。未來當團隊要做「忘記使用者名稱」之類的功能時，只要把這份 spec 複製一份再修改即可。

產品負責人的角色，從「口頭傳達需求」演進為「建立明確的規格 primitives」。協調上的好處是：每位團隊成員都讀同一份規格，不會再出現「我以為你說的是……」這種落差。

**第 0–1 週：架構師／技術主管 —— 技術規劃**

技術主管會審閱 `password-reset.spec.md`，並做出架構決策。例如：使用有時效性的 JWT token 作為重設連結，token 儲存在具 TTL 的 Redis 中，整合既有的郵件服務，並加入 rate limiting 避免濫用。

他不會只在會議中講過就算，而是建立：

```bash
/speckit.plan Use JWT tokens with 1-hour expiration for reset links. Store in Redis 
with TTL. Email service sends reset link. Rate limit: max 3 requests per hour per email. 
New endpoints: POST /auth/reset-request, POST /auth/reset-confirm. Follows existing auth 
patterns from auth-patterns.instructions.md.
```

輸出是一份技術計畫，記錄元件拆分、技術選擇與 API 合約。這份文件可以是 `password-reset-plan.md`，也可以被合併進 `auth.context.md` 供未來參考。

更進一步地，技術主管會更新共享的 instructions。假設在上一個 Sprint 實作 OAuth 時，他發現了一個好的安全 token 處理模式，於是建立 `token-security.instructions.md`：

```markdown
---
applyTo: "**/auth/**"
---
# Secure Token Handling Standards

## Token Generation
- Use crypto.randomBytes() for token generation
- Minimum 32-byte entropy
- Store hashed version in database

## Token Validation  
- Always check expiration before use
- Invalidate after single use (for reset flows)
- Rate limit token generation endpoints
```

未來所有與驗證相關的實作——不論是誰寫、用哪一個 agent 實作——都會自動繼承這個模式。技術主管的架構知識，透過 primitives 變成整個團隊的知識。

**第 1 週：Scrum Master —— 工作流程推動者**

Scrum Master 會協助 Sprint 規劃。在有了 spec 與 plan 之後，團隊會把工作拆解成任務：

```bash
/speckit.tasks
```

輸出會是一組 GitHub Issues：
- Task 1: Add password reset token schema to database
- Task 2: Implement JWT token generation for reset flow  
- Task 3: Create POST /auth/reset-request endpoint
- Task 4: Build email template for reset link
- Task 5: Create POST /auth/reset-confirm endpoint
- Task 6: Add rate limiting middleware
- Task 7: Frontend: password reset request form
- Task 8: Frontend: new password entry form
- Task 9: Integration tests for reset flow

Scrum Master 的角色，從「在會議中協助大家討論拆任務」演化成「協調 spec-driven 的任務生成流程，並確認各項驗證關卡清楚存在」。他會檢查：架構是否已被核准？依賴關係是否在 GitHub Projects 裡清晰呈現？每個任務的驗收標準是否具體？

結果是：更少時間花在會議上，更多時間用來確保工作流程產出的工件是高品質的。

**第 1–2 週：開發者 —— 實作與委派**

開發者會依 GitHub Projects 上的依賴關係領取任務。開發者 A 負責後端相關項目，開發者 B 負責前端。每個人都可以選擇自行實作，或是委派給 agent：

開發者 A：

```bash
apm run implement-from-spec --param spec="password-reset.spec.md" --param task="3"
```

他自訂的 `.prompt.md` 工作流程會：
1. 載入對應的 spec 與 plan 作為上下文
2. 讀取 `token-security.instructions.md`（透過 `applyTo` 模式自動生效）  
3. 參考 `auth.context.md` 中既有的驗證模式
4. 生成含有測試的實作
5. 建立一個 PR，並在描述中標明對應 spec 與任務

開發者 B 則可以直接使用 Spec-Kit：

```bash
/speckit.implement
```

結果是一樣的：agent 會根據所有相關 primitives 產生實作與測試，並建立準備好供審查的 PR。

重要的是：開發者不只是 primitives 的使用者，也是它們的貢獻者。假設開發者 A 發現密碼重設流程在安全上需要額外的稽核紀錄，他就會更新 `security-audit.instructions.md`，把這個需求加入其中。未來每一個相關實作，都會自動包含這項規範。

**第 2 週：QA／安全團隊 —— 驗證 primitives**

QA 會審查密碼重設實作。傳統上，他們會為每一個功能寫一份測試計畫；在這裡，他們則會建立一個可重用的測試工作流程：

`password-reset-test.prompt.md`：

```markdown
# Password Reset Test Workflow

## Security Validation
- [ ] Verify token expires after 1 hour
- [ ] Confirm token invalidates after use  
- [ ] Check rate limiting prevents abuse
- [ ] Validate email contains HTTPS link only

## Functionality Testing  
- [ ] User receives email with reset link
- [ ] Token successfully resets password
- [ ] Old password no longer works
- [ ] User can login with new password

## Edge Cases
- [ ] Invalid token returns appropriate error
- [ ] Expired token returns appropriate error
- [ ] Non-existent email handled gracefully
```

這個 workflow 會變成未來可重用的測試工具。下次再實作與密碼相關的功能時，QA 只需要再次執行這個 workflow，而不必從頭設計測試案例。如此一來，驗證在不同功能間就能保持一致性。

安全團隊也可以為驗證相關功能建立 `security-review-checklist.prompt.md`。之後，所有與驗證相關的 PR 在審查時，都可以套用這份系統化的檢查清單。驗證依然是人工進行，但由可重用的 primitives 提供結構化引導。

### 複合效應

回顧這整個 Sprint，可以看到發生了什麼事：

- **產品負責人** 建立了 `password-reset.spec.md` → 成為未來類似功能的規格模板
- **技術主管** 建立了 `token-security.instructions.md` → 變成所有未來驗證實作自動繼承的模式  
- **開發者** 更新了 `security-audit.instructions.md` → 提升所有實作在合規面向上的品質
- **QA** 建立了 `password-reset-test.prompt.md` → 變成可重用的驗證工作流程

團隊的 primitive 函式庫隨之擴張。當下一個 Sprint 要實作「忘記使用者名稱」功能時：
- 可以複製並調整 `password-reset.spec.md`（更快寫出規格）
- 自動繼承 `token-security.instructions.md`（安全模式不必再討論一次）  
- 透過更新後的 `security-audit.instructions.md` 自動包含稽核紀錄（合規直接內建）
- 重用 `password-reset-test.prompt.md`（測試標準一致）

每一個 Sprint 都會讓下一個 Sprint 變得更快、更可靠。這就是**團隊層級的複合智慧**：每個角色仍然保持專業分工，但輸出的成果會以 primitives 的形式被累積下來。

### AI Native Development 中的角色清晰度

關鍵洞見在於：**AI Native Development 並不會模糊角色邊界，反而讓責任更清楚。**

- **產品負責人（Product Owners）** 負責「What」→ 建立 `.spec.md` 檔案  
- **架構師（Architects）** 負責「How」→ 建立技術計畫與 `.instructions.md` 模式
- **Scrum Masters** 負責「Workflow」→ 促成 spec-driven 儀式並確保驗證關卡存在
- **開發者（Developers）** 負責「Execution」→ 實作、委派並持續優化工作流程
- **QA／安全團隊（QA/Security）** 負責「Validation」→ 建立驗證 primitives 並維持品質關卡

每一個角色，都會為 primitive 函式庫做出貢獻；每一個 primitive，都會放大整個團隊的能力。因為 primitives 取代了大量同步溝通，協調開銷也就隨之下降。

這就是團隊如何在不更改角色分工的前提下，將 AI Native Development 擴展到整個組織：**不是重塑角色，而是讓各角色的輸出，從一次性的溝通，轉變為可持續重用的 primitives。**

## F. 知識分享與團隊智慧

個別開發者會透過實戰經驗不斷精煉自己的 primitives——發現更好的模式、辨識新的邊界情境、優化工作流程。上一章節說明了各個角色如何在 Sprint 中產生 primitives；本節則關注一個問題：這些個人的發現，如何提升整個團隊的智慧？當某人離開時，知識如何不流失？智慧又如何在一個又一個 Sprint 中持續累積？

答案是：將**primitive 精煉**系統性地嵌入既有的敏捷儀式中，再搭配 APM 進行跨團隊的知識分享。

### Sprint 回顧：Primitive 精煉引擎

傳統的 Sprint retrospective，會列出一些流程層面的改進意見：「我們應該要有更好的 API 文件」、「Code review 花太久」、「需求一開始不夠清楚」。這些觀察常常停留在會議記錄裡，很少真正轉化成系統性的改變。

結合 primitives 的 spec-driven 回顧，則會產生具體、可執行、也可強制落實的改善：

**回顧模式：**

1. **檢視 primitives 的效果**：哪些 `.instructions.md` 對 agents 的引導很好？哪些 specs 太模糊？哪些工作流程在實作時失靈？
2. **找出可精煉的機會**：agent 是否誤解了某個安全需求？→ 更新 `security-standards.instructions.md`，讓描述更清楚。實作 workflow 是否漏掉某些邊界情境？→ 在 `implement-from-spec.prompt.md` 中加入新的檢查步驟。
3. **在 `.memory.md` 中記錄反模式**：把失敗的嘗試寫下來，讓未來避免重蹈覆轍。例如：「曾嘗試使用 session storage 儲存 password reset tokens —— 安全性不足。未來一律使用具 TTL 的 Redis。」
4. **把成功模式提升到共享函式庫**：若有開發者找到很好的錯誤處理模式，就把它抽出來放進 `error-handling.instructions.md`，讓未來所有實作都能繼承它。
5. **更新 specs 以利重用**：當一個功能順利完成，對應的 spec 就可以被標記為模板，例如 `user-auth.spec.md [TEMPLATE]`，供未來的驗證功能作為起點。

這樣的回顧，產出的是實打實的改動：更新後的 primitive 檔案會被提交進儲存庫。下一個 Sprint 一開始，團隊就已經建立在更好的 primitives 之上，智慧因而持續複利成長。

### 集中式 primitive 函式庫：單一真實來源

（後續內容請依據英文原文的剩餘段落，持續以同樣的一對一原則翻譯與維護。）
