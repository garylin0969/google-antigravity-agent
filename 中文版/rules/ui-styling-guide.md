---
trigger: always_on
description: 當建構 UI 時啟動。強制使用 Tailwind CSS、Shadcn UI / Radix UI 元件模式及表單驗證標準。
---

# UI 與樣式指南

## 1. 樣式（Tailwind CSS）

- **一律**使用 Tailwind CSS 工具類別。避免自訂 CSS 檔案或 `<style>` 標籤。
- 遵循 **Mobile-First** 設計原則。
- 使用標準 Tailwind 工具類別（例如：`flex items-center justify-between`）。

## 2. 元件庫

- 使用 **Shadcn UI** 提供一致、預建的設計元件。
- 使用 **Radix UI** 原語 (Primitives) 提供無樣式但具無障礙功能的基礎元件。
- 使用**組合 (Composition)** 模式建立模組化、可重用的元件。

## 3. 表單與驗證

- **驗證**：使用 **Zod** 進行 Schema 驗證。
- **狀態管理**：使用 **React Hook Form** 管理表單狀態。
- **使用者體驗**：提供清晰、即時的錯誤訊息與載入狀態。
