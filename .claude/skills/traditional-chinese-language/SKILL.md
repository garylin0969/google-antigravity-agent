---
name: traditional-chinese-language
description: This skill is always active. Always respond, explain, and ask in Traditional Chinese (Taiwan) for all conversations in this project. Never switch to English for explanations unless explicitly asked.
user-invocable: false
---

# Traditional Chinese Language Convention

All responses, questions, and communication must be written in **Traditional Chinese (Taiwan)**.

## Rules

- **Always on**: Apply this rule to every response without exception, regardless of the language the user writes in.
- **Language**: Use Traditional Chinese (繁體中文) at all times.
- **Locale**: Follow Taiwan conventions (e.g., 「軟體」not 「软件」, 「檔案」not 「文件」).
- **Dev terms**: Common development terms may remain in English when they are industry-standard and translation would sound unnatural. Examples: component, hook, props, state, render, API, endpoint, payload, PR, commit, branch, deploy, debug, cache, token, middleware, callback, interface, type, generic.
- **Code**: Variable names, function names, and code itself remain in English. All explanations, summaries, and questions must be in Traditional Chinese.
- **Tone**: Use natural, clear Traditional Chinese. Avoid forced translation of terms that are universally used in English.

## Examples

✅ Correct:

> 這個 component 使用了 `useState` hook 來管理購物車的 state。你是否要我同時處理折扣邏輯？

✅ Also correct (dev terms stay in English):

> 這個 API endpoint 回傳的 payload 結構有問題，建議在 middleware 加上驗證。

❌ Incorrect (English response):

> This component uses useState to manage cart state.

❌ Incorrect (Simplified Chinese):

> 这个组件使用了 useState 来管理购物车的状态。
