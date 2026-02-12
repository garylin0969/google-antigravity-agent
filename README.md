# Google Antigravity Agent 配置指南

這份文件旨在幫助新手快速上手 **Google Antigravity Agent** 的配置。

核心在於設定好 **Rules (規則)** 與 **Skills (技能)**，讓 Agent 依據你定義的行為準則生成程式碼與回答問題。

> 📚 **官方文件參考**：
>
> - [Rules & Workflows 文件](https://antigravity.google/docs/rules-workflows)
> - [Skills 文件](https://antigravity.google/docs/skills)

---

## 📋 目錄

- [🚀 Rules (規則)](#-rules-規則)
    - [什麼是 Rule？](#什麼是-rule)
    - [檔案位置](#1-檔案位置-必填)
    - [檔案格式規範](#2-檔案格式規範)
    - [Rule 範例](#3-rule-範例)
- [🛠️ Skills (技能)](#️-skills-技能)
    - [什麼是 Skill？](#什麼是-skill)
    - [目錄結構](#1-目錄結構)
    - [SKILL.md 寫法](#2-skillmd-寫法-極重要)
    - [選填資料夾](#3-選填資料夾的使用情境)
- [📂 本專案範例](#-本專案範例)
- [🎯 快速入門 Checklist](#-快速入門-checklist)
- [❓ 常見問題 FAQ](#-常見問題-faq)

---

## 🚀 Rules (規則)

### 什麼是 Rule？

**Rule** 是 Agent 在生成內容或回答時必須遵守的「家規」。

你可以把它想像成對 Agent 的一份「員工規範」——告訴它什麼可以做、什麼不能做、該用什麼格式輸出等。

### 1. 檔案位置 (必填)

所有規則檔案必須放在：

```
.agent/rules/*.md
```

> 💡 **提示**：檔名可以自由命名，但建議使用有意義的 kebab-case，例如 `code-style.md`、`commit-convention.md`。

### 2. 檔案格式規範

Rule 檔案是純 Markdown 檔案，格式非常自由。

#### 🔴 內文 (Required)

規則的本體是 Markdown 內文。你必須清楚用文字描述「要做什麼」與「不該做什麼」。Agent 會讀取這些文字來調整它的行為。

**內文建議包含：**

- 規則的目的與適用情境
- 具體的規範條目（用列表或表格呈現更清晰）
- 正確與錯誤範例（有 Code Block 更佳）

#### 🟢 Frontmatter (Optional)

在檔案頂部的 YAML 區塊並非官方強制要求，但可以幫助你管理規則。

```yaml
---
name: my-rule-name # [選填] 規則名稱，僅供管理方便
description: 描述這個規則... # [選填] 簡短描述
---
```

> ⚠️ **注意**：本專案中部分檔案使用 `trigger` 欄位僅作為開發者方便管理的標記，Agent 主要依賴**語意理解**來判斷何時應用規則。

### 3. Rule 範例

以下是一個簡化版的 Rule 檔案範例：

```markdown
---
name: commit-convention
description: 規範 Git Commit Message 格式
---

# Git Commit Message 規範

所有 Commit Message 必須遵循 Conventional Commits 格式。

## 格式

\`\`\`
<type>(<scope>): <subject>
\`\`\`

## 允許的 Type

| Type       | 說明                     |
| ---------- | ------------------------ |
| `feat`     | 新功能                   |
| `fix`      | 修復 Bug                 |
| `docs`     | 文件更新                 |
| `refactor` | 重構（不影響功能的修改） |

## 範例

✅ 正確：`feat(auth): add login API`
❌ 錯誤：`Added login`
```

---

## 🛠️ Skills (技能)

### 什麼是 Skill？

**Skill** 是 Agent 的擴充能力，讓它能執行特定任務（如查詢文件、執行腳本、依照模板生成程式碼）。

**設定 Skills 時，格式要求比 Rules 嚴格許多，請務必遵守。**

### 1. 目錄結構

**一個 Skill = 一個資料夾**

路徑：`.agent/skills/<skill-name>/`

| 檔案/資料夾      | 狀態                   | 說明                                           |
| :--------------- | :--------------------- | :--------------------------------------------- |
| **`SKILL.md`**   | 🔴 **必要 (Required)** | 技能的核心定義檔。**沒有這個檔案，技能無效。** |
| **`resources/`** | 🟢 **選填 (Optional)** | 靜態參考資料 (如 API 文件、錯誤代碼表)         |
| **`templates/`** | 🟢 **選填 (Optional)** | 程式碼範本 (如 React Component 模板)           |
| **`scripts/`**   | 🟢 **選填 (Optional)** | 執行腳本 (如 Shell Script, Python 腳本)        |

**完整結構範例：**

```
.agent/
└── skills/
    └── my-skill-name/
        ├── SKILL.md          # 🔴 必填：技能定義檔
        ├── resources/        # 🟢 選填：靜態資料
        │   └── api-spec.json
        ├── templates/        # 🟢 選填：程式碼範本
        │   └── component.tsx.hbs
        └── scripts/          # 🟢 選填：執行腳本
            └── deploy.sh
```

### 2. `SKILL.md` 寫法 (極重要)

這是技能的「身分證」。根據官方文件，**description 是唯一絕對必填的欄位**。

#### Frontmatter (檔頭設定)

```yaml
---
name: my-skill-name # 🟢 [選填] 技能名稱。若未填寫，預設會使用資料夾名稱。
description: ... # 🔴 [必填] 技能描述。Agent 完全依賴這段文字來判斷何時使用此技能。
---
```

> **⚠️ 重點提醒：**
>
> `description` 是核心中的核心！Agent **不會通靈**，你必須在這裡清楚描述：
>
> 1. **什麼情況下**要使用這個技能（觸發條件）
> 2. **用來做什麼**（技能目的）
>
> 寫得越明確，Agent 越能準確判斷何時使用。

#### Body (內文)

Markdown 內文必須包含明確的執行步驟，告訴 Agent「拿到這個技能後，要怎麼用」。

**內文建議包含：**

- 執行流程（Step by Step）
- 輸出規範或格式要求
- 相關檔案的使用說明（如有 resources, templates, scripts）

### 3. 選填資料夾的使用情境

雖然以下資料夾是選填的，但善用它們能讓技能更強大：

#### 📚 `resources/` (知識庫)

- **用途**：存放 Agent 需要「閱讀」的靜態資料。
- **情境**：
    - 你需要 Agent 遵守公司特定的 Error Code 處理方式 ➡ 放 `error-codes.md`
    - 你需要 Agent 依照特定的 API 規格寫 Code ➡ 放 `api-swagger.json`

#### 📄 `templates/` (模具)

- **用途**：存放 Agent 用來「生成」檔案的範本。
- **情境**：
    - 你希望所有 React Component 都長得一樣 ➡ 放 `component.tsx.hbs`
    - 你希望 Pull Request 的描述格式統一 ➡ 放 `pr-template.md`

#### 🔧 `scripts/` (工具)

- **用途**：存放 Agent 用來「執行」的程式腳本。
- **情境**：
    - 部署流程很複雜，包含 git 操作與 api 呼叫 ➡ 寫成 `deploy.sh` 讓 Agent 執行
    - 需要對資料庫進行大量運算 ➡ 寫成 `migration.py` 讓 Agent 執行

---

## 📂 本專案範例

本專案包含完整的 Rules 與 Skills 範例，供你參考與學習。

### Rules 範例

本專案的 Rules 以**英文撰寫**（方便 AI 編輯器理解），並在 `中文版/` 資料夾提供對應的繁體中文版本。

| 檔案                         | 說明                                                                  |
| :--------------------------- | :-------------------------------------------------------------------- |
| `coding-standards.md`        | 核心開發理念、工作流程、語法風格、無障礙、TypeScript 最佳實踐         |
| `reactjs-nextjs-patterns.md` | React.js 最佳實踐、Next.js App Router 慣例、Server Component 優先策略 |
| `component-structure.md`     | Atomic Design 元件架構與檔案組成規範                                  |
| `file-naming-convention.md`  | 全域 kebab-case 檔案命名規範                                          |
| `jsdoc-convention.md`        | Google Style 繁體中文 JSDoc 註解標準                                  |
| `ui-styling-guide.md`        | Tailwind CSS + Shadcn UI + Radix UI + 表單驗證                        |

### Skills 範例

| 資料夾                              | 說明                                                     |
| :---------------------------------- | :------------------------------------------------------- |
| `.agent/skills/nextjs-docs-lookup/` | 強制 Agent 查詢 Next.js 官方文件來回答問題，確保資訊正確 |

---

## 🎯 快速入門 Checklist

新專案要加入 Agent 配置？照著這份清單走就對了：

### Step 1: 建立目錄結構

```bash
mkdir -p .agent/rules
mkdir -p .agent/skills
```

### Step 2: 新增你的第一個 Rule

在 `.agent/rules/` 建立一個 `.md` 檔案，例如 `code-style.md`：

```markdown
# 程式碼風格規範

- 所有變數命名使用 camelCase
- 所有函式必須加上 JSDoc 註解
```

### Step 3: 新增你的第一個 Skill (如有需要)

1. 建立 Skill 資料夾：`mkdir -p .agent/skills/my-first-skill`
2. 建立核心檔案：`.agent/skills/my-first-skill/SKILL.md`

```yaml
---
name: my-first-skill
description: 當使用者詢問 XXX 時啟動，用於 YYY。
---
# My First Skill

## 執行步驟

1. 第一步做什麼
2. 第二步做什麼
```

### Step 4: 測試

跟 Agent 對話，觀察它是否有套用你的 Rules 與 Skills！

---

## ❓ 常見問題 FAQ

### Q1: Rule 跟 Skill 有什麼差別？

| 項目 | Rule (規則)                       | Skill (技能)                    |
| ---- | --------------------------------- | ------------------------------- |
| 性質 | 行為準則 / 限制條件               | 擴充能力 / 執行任務             |
| 用途 | 限制 Agent「怎麼做」              | 賦予 Agent「能做什麼」          |
| 格式 | 單一 `.md` 檔案                   | 一個資料夾 + `SKILL.md`         |
| 觸發 | 根據語意自動套用                  | 根據 `description` 判斷是否使用 |
| 範例 | 命名規範、程式碼風格、Commit 格式 | 查文件、跑腳本、依模板生成檔案  |

### Q2: 為什麼我的 Skill 沒有被觸發？

1. **檢查 `description`**：是否清楚描述了觸發條件？
2. **檢查資料夾結構**：是否有 `SKILL.md` 這個檔案？（大小寫敏感！）
3. **嘗試更明確的對話**：在對話中直接提及關鍵字

### Q3: 我可以有多少個 Rules / Skills？

沒有硬性限制，但建議：

- 每個 Rule 專注於一件事，避免過於龐雜
- Skill 數量不宜過多，以免 Agent 判斷困難

### Q4: 檔案可以用中文命名嗎？

**不建議**。請使用 `kebab-case` 英文命名以確保跨平台相容性。

---

## 📝 附錄：專案結構總覽

```
.agent/
├── rules/                                  # 📋 規則目錄（英文版 - 給 AI 編輯器）
│   ├── coding-standards.md                 # 編碼標準
│   ├── reactjs-nextjs-patterns.md          # React.js & Next.js 開發模式
│   ├── component-structure.md              # 元件結構（Atomic Design）
│   ├── file-naming-convention.md           # 檔案命名規範
│   ├── jsdoc-convention.md                 # JSDoc 註解規範
│   └── ui-styling-guide.md                 # UI 與樣式指南
└── skills/                                 # 🧰 技能目錄
    └── nextjs-docs-lookup/
        └── SKILL.md                        # Next.js 文件檢索技能

中文版/
├── rules/                                  # 📋 規則目錄（繁體中文版）
│   ├── coding-standards.md
│   ├── reactjs-nextjs-patterns.md
│   ├── component-structure.md
│   ├── file-naming-convention.md
│   ├── jsdoc-convention.md
│   └── ui-styling-guide.md
└── skills/
    └── nextjs-docs-lookup/
        └── SKILL.md
```

---

> 🎉 **配置完成後，就可以開始享受 Agent 帶來的高效開發體驗了！**
>
> 如有問題，歡迎查閱官方文件或回到本專案參考範例。
