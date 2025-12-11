---
layout: home
title: "GitHub Copilot 精通指南：AI Native Development"
permalink: /zh-tw/
lang: zh-TW
---

<div style="margin: 32px 0;" markdown="1">

**學習如何建立可靠的 AI 系統，讓它自主編寫程式碼**

*這份指南為開發者提供什麼*（2 分鐘閱讀）：

- **最大可靠性**：學習系統化方法，消除 AI 的不一致性，每次都能交付專業品質的結果
- **多 Agent 委派**：從單一 prompt 進階到自信地將完整編碼任務委派給 GitHub Coding Agents
- **經過驗證的工程方法**：應用結構化方法論（Markdown Prompt Engineering、Agent Primitives、Context Engineering）獲得可預測的結果
- **複合生產力**：建立可重用的 AI 配置，隨著時間改進並倍增你的開發能力
- **團隊轉型**：將這些經過實戰驗證的模式擴展到整個組織，獲得指數級的生產力提升

> **社群資源：** 探索 [Awesome GitHub Copilot](https://github.com/github/awesome-copilot) 儲存庫，獲取數百個社群貢獻的 instructions、prompts 和 chat modes，涵蓋所有主要語言和框架。

</div>

## 選擇你的學習路徑

<div class="learning-paths">
  <a href="docs/concepts/" class="path-card">
    <div class="path-title">核心概念</div>
    <div class="path-description">理解 Agent Primitives 背後的工程原則</div>
    <div class="path-meta">15-20 分鐘 • 理論與基礎</div>
    <div class="path-link">了解更多</div>
  </a>

  <a href="docs/getting-started/" class="path-card">
    <div class="path-title">快速開始</div>
    <div class="path-description">建立你的第一個 Agent Primitives 並立即看到成果</div>
    <div class="path-meta">15-20 分鐘 • 實作練習</div>
    <div class="path-link">了解更多</div>
  </a>

  <a href="docs/tooling/" class="path-card">
    <div class="path-title">工具生態</div>
    <div class="path-description">透過 runtime、context compilation 和套件管理擴展 Agent Primitives</div>
    <div class="path-meta">12-15 分鐘 • 基礎設施與擴展</div>
    <div class="path-link">了解更多</div>
  </a>

  <a href="docs/agent-delegation/" class="path-card">
    <div class="path-title">Agent 委派</div>
    <div class="path-description">精通非同步委派和多 agent 協調</div>
    <div class="path-meta">20-25 分鐘 • 進階模式</div>
    <div class="path-link">了解更多</div>
  </a>

  <a href="docs/team-adoption/" class="path-card">
    <div class="path-title">團隊導入</div>
    <div class="path-description">將 AI Native Development 擴展到整個組織</div>
    <div class="path-meta">15-20 分鐘 • 團隊與領導</div>
    <div class="path-link">了解更多</div>
  </a>

  <a href="docs/reference/" class="path-card">
    <div class="path-title">參考資料</div>
    <div class="path-description">清單、指南和持續參考的文件</div>
    <div class="path-meta">5-10 分鐘 • 快速查閱</div>
    <div class="path-link">了解更多</div>
  </a>
</div>

## 核心心智模型

將 AI Native Development 想像成**專業軟體開發實踐**：

- **Markdown Prompt Engineering** = AI 互動的編碼標準
- **Agent Primitives** = 可重用的函式庫和配置
- **Context Engineering** = 記憶體和效能優化

*準備好轉型你的 AI 開發工作流程了嗎？選擇上方的學習路徑，立即開始建立更可靠、一致的 AI 互動。*

## AI Native Development 成熟度

大多數開發者一開始都是手動監督每個 AI 互動 — 為每個任務撰寫一次性 prompts，每次都從頭開始。這造成了一個瓶頸，你的參與對 AI 任務的成功總是必要的。

**當你從監督轉向架構時，轉變就發生了。** 不再管理個別的 AI 對話，而是工程化可重用的系統，將整個工作流程委派給 AI agents。

這個成熟度旅程代表了從被動 AI 使用到主動 AI 工程的核心思維轉變：

<div class="maturity-timeline">
  <div class="maturity-stage maturity-from">
    <div class="stage-content">
      <div class="stage-header">
        <div class="stage-number">1</div>
        <div class="stage-label">初學者</div>
      </div>
      <h3>手動 Agent 監督</h3>
      <p class="stage-subtitle">你監督每個 AI 互動</p>
      <ul class="stage-points">
        <li>為每個任務撰寫一次性 prompts</li>
        <li>手動引導每次對話</li>
        <li>每次都從頭開始</li>
      </ul>
      <div class="stage-outcome">
        <strong>你是瓶頸</strong> - 每個 AI 任務都需要你的關注
      </div>
    </div>
  </div>

  <div class="timeline-connector">
    <div class="connector-arrow">→</div>
  </div>

  <div class="maturity-stage maturity-to">
    <div class="stage-content">
      <div class="stage-header">
        <div class="stage-number">2</div>
        <div class="stage-label">專家</div>
      </div>
      <h3>工程化 Agent 委派</h3>
      <p class="stage-subtitle">你設計系統架構，AI 執行</p>
      <ul class="stage-points">
        <li>建立可重用的 <strong>Agent Primitives</strong></li>
        <li>一次工程化 context，隨處重用</li>
        <li>將完整工作流程委派給 AI</li>
      </ul>
      <div class="stage-outcome">
        <strong>你是架構師</strong> - AI 自主處理執行
      </div>
    </div>
  </div>
</div>

## 貢獻

> *「未來屬於能夠架構 AI 系統的開發者，而不僅僅是提示它們的人。」*

**這是前沿工作。** AI Native Development 正在快速演進，今天有效的模式明天會被優化。這就是為什麼這份指南需要社群創新。

**你的貢獻塑造這個領域。** 無論你發現新的 Agent Primitive 模式、優化現有工作流程，還是分享突破性的洞見 — 每一份貢獻都推進我們的集體理解，並讓你被列為這個持續演進知識庫的共同作者。

**準備好引領轉型了嗎？**

<div class="cta-buttons">
  <a href="docs/concepts/" class="btn-primary">閱讀指南 →</a>
  <a href="https://github.com/chunkai1312/awesome-ai-native/blob/main/CONTRIBUTING.md" class="github-btn"><span class="github-text">貢獻你的洞見 →</span></a>
</div>

*最可靠的 AI 系統是由社群建立的，而不是個人。*
