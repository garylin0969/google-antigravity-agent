---
name: jsdoc-convention
description: 當撰寫、重構或解釋 TypeScript/JavaScript 程式碼時啟動。強制為所有導出的函式、類別、介面與元件添加 Google Style 的繁體中文 JSDoc 註解。
---

# JSDoc 註解規範（Google Style）

為了確保程式碼的可讀性與 IDE 支援度，所有 Exported（導出）的程式碼實體必須遵循 Google JavaScript Style Guide 的 JSDoc 規範。所有說明文字必須使用**繁體中文（台灣）**。

> 📚 **官方參考**：[Google JavaScript Style Guide - JSDoc](https://google.github.io/styleguide/jsguide.html#jsdoc)

## 1. 核心原則

- **語言**：所有說明文字必須使用**繁體中文**（台灣習慣用語）。
- **格式**：必須使用 `/** ... */` 多行註解格式。
- **時機**：在定義任何 `export` 的 Function、Component、Interface、Type、Class 之前，必須加上註解。

## 2. 撰寫範例

### A. 函式與工具

註解第一行應為簡短的摘要，若有詳細說明請空一行再寫。

```typescript
/**
 * 計算購物車的總金額，並包含稅率運算。
 *
 * 此函式會自動過濾掉無效的商品項目，並應用當前的優惠券折扣。
 */
export const calculateTotal = (items: CartItem[], taxRate: number = 0.05, couponCode?: string): number => {
    // ...
};
```

### B. React 元件

必須清楚說明元件的職責。

```tsx
/**
 * 使用者個人資料卡片元件。
 *
 * 負責顯示使用者的頭像、名稱以及簡介。
 * 點擊卡片時會觸發導航至使用者詳情頁面。
 */
const UserProfileCard = ({ userId, name, avatarUrl, onClick }: UserProfileCardProps) => {
    // ...
};

export default UserProfileCard;
```

### C. 介面與型別

每個屬性上方都應有單行說明。

```typescript
/**
 * 定義 API 回傳的標準錯誤格式
 */
interface ApiErrorResponse {
    /** 錯誤代碼 (如: 404, 500) */
    code: number;
    /** 給使用者看的錯誤訊息 (繁體中文) */
    message: string;
    /** 除錯用的詳細堆疊資訊 (僅在開發環境回傳) */
    stack?: string;
}
```

## 3. 執行檢查

生成程式碼後，請檢查：

- [ ] 註解是否位於程式碼正上方？
- [ ] 說明文字是否通順且為繁體中文？
