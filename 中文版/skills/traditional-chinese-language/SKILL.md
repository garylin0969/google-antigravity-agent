---
name: traditional-chinese-language
description: 此技能永遠啟動。無論使用者用何種語言提問，所有回應、解釋與提問一律使用繁體中文（台灣）。除非使用者明確要求，否則不切換為英文回覆。
user-invocable: false
---

# 語言規範：繁體中文（台灣）

所有回應、提問與溝通一律使用**繁體中文（台灣）**。

## 規則

- **永遠啟動**：無論使用者用何種語言提問，每一則回應都必須套用此規則。
- **語言**：始終使用繁體中文。
- **地區慣用語**：遵循台灣用語（例如：「軟體」而非「软件」、「檔案」而非「文件」、「網路」而非「网络」）。
- **開發慣用詞**：業界通用的英文開發術語可保持英文，強行翻譯反而不自然。例如：component、hook、props、state、render、API、endpoint、payload、PR、commit、branch、deploy、debug、cache、token、middleware、callback、interface、type、generic。
- **程式碼本體**：變數名稱、函式名稱與程式碼本體保持英文，但所有說明、摘要與提問必須以繁體中文撰寫。
- **語氣**：使用自然流暢的繁體中文，避免強行翻譯業界慣用的英文術語。

## 範例

✅ 正確：

> 這個 component 使用了 `useState` hook 來管理購物車的 state。你是否要我同時處理折扣邏輯？

✅ 也正確（開發慣用詞保持英文）：

> 這個 API endpoint 回傳的 payload 結構有問題，建議在 middleware 加上驗證。

❌ 錯誤（英文回覆）：

> This component uses useState to manage cart state.

❌ 錯誤（簡體中文）：

> 这个组件使用了 useState 来管理购物车的状态。
