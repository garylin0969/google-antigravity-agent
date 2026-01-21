---
name: kebab-naming-enforcer
description: 當使用者要求建立或修改檔案時啟動。強制執行全域 kebab-case 命名與檔案結構規範。
---

# 全域檔案命名與結構規範

為了保持專案檔案系統的一致性，所有檔案名稱與資料夾名稱都必須嚴格遵循 **kebab-case** 命名法則。

## 1. 核心命名法則 (Core Naming Rule)

所有檔案名稱與資料夾名稱，必須將程式碼中的 `camelCase` 或 `PascalCase` 轉換為 **`kebab-case`**。

- **變數/函式名 (Code)**: `useWindowSize` ➡ **檔案名 (File)**: `use-window-size.ts`
- **類別名 (Code)**: `AuthService` ➡ **檔案名 (File)**: `auth-service.ts`
- **工具名 (Code)**: `dateFormat` ➡ **檔案名 (File)**: `date-format.ts`

## 2. 各類別詳細規範 (Category Specifications)

### A. Custom Hooks (`/hooks`)

Hook 檔案必須保留 `use-` 前綴，並全小寫。

- ✅ 正確：`hooks/use-auth-listener.ts`
- ❌ 錯誤：`hooks/useAuthListener.ts`

### B. Utilities (`/utils` 或 `/lib`)

工具函式若為單一檔案，直接使用 kebab-case；若為資料夾分類，資料夾亦須為 kebab-case。

- ✅ 正確：`utils/string-helper.ts`
- ✅ 正確：`utils/api-formatters/date-parser.ts`

### C. Services (`/services`)

API 服務層通常對應特定的業務邏輯，檔案名應描述該服務功能。

- ✅ 正確：`services/user-api.ts`
- ✅ 正確：`services/payment-gateway.ts`

## 3. 執行檢查清單 (Execution Checklist)

當你生成上述類型的檔案時，請執行以下檢查：

1.  **檢查檔名**：是否有大寫字母？若有，請轉為小寫並用連字號 `-` 分隔。
2.  **檢查資料夾**：若需要建立新資料夾，確保資料夾名稱也是 kebab-case。
3.  **內容對應**：雖然檔名是 `kebab-case`，但檔案內的 `export` 變數或函式名稱仍維持 JS/TS 標準的 `camelCase` 或 `PascalCase`。

---

## 範例對照表

| 類型        | 程式碼內命名 (Export)                  | 檔案路徑與命名 (File System)   |
| :---------- | :------------------------------------- | :----------------------------- |
| **Hook**    | `export const useScrollPosition = ...` | `hooks/use-scroll-position.ts` |
| **Service** | `export const OrderService = ...`      | `services/order-service.ts`    |
| **Util**    | `export function formatCurrency() ...` | `utils/format-currency.ts`     |
| **Type**    | `export interface UserProfile ...`     | `types/user-profile.ts`        |
