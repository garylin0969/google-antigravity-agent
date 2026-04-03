# Agent Skills 配置指南

這份文件旨在幫助你快速上手 **Agent Skills（代理技能）** 的配置。

**Agent Skills 是一個開放標準**（由 Anthropic 開發並公開），不限於單一工具，可跨多種 AI 工具使用。

核心在於設定好 **Custom Agents（自訂代理）** 與 **Skills（技能）**，讓 AI 依據你定義的角色與能力生成程式碼並執行任務。

> 📚 **官方文件參考**：
>
> - [Agent Skills 開放標準](https://agentskills.io/)
> - [Agent Skills Quickstart](https://agentskills.io/skill-creation/quickstart)
> - [VS Code - Custom Agents](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
> - [VS Code - Agent Skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
> - [Claude Code - Skills](https://code.claude.com/docs/en/skills)

---

## 🌍 跨工具支援

Agent Skills 是 [agentskills.io](https://agentskills.io/) 開放標準，**已被以下工具官方支援**：

| 工具                       | 說明                                                                   |
| :------------------------- | :--------------------------------------------------------------------- |
| **VS Code GitHub Copilot** | 完整支援，讀取 `.agents/skills/`、`.github/skills/`、`.claude/skills/` |
| **Claude Code**            | 完整支援，讀取 `.claude/skills/`                                       |
| **Goose**                  | Block 開發的 AI 代理工具                                               |
| **JetBrains Junie**        | JetBrains AI 助理                                                      |
| **TRAE**                   | ByteDance 開發的 AI IDE                                                |
| **Factory**                | AI 軟體開發平台                                                        |
| **Spring AI**              | Java AI 開發框架                                                       |
| **OpenAI Codex**           | OpenAI 的 AI 開發工具                                                  |
| 以及更多...                | Firebender、Qodo、Emdash、Databricks、Snowflake 等                     |

> ⚠️ **注意**：Gemini CLI 等工具目前**不在官方支援清單**，無法自動讀取 SKILL.md 格式。

### 重要：各工具讀取的目錄不同

| 路徑                 | VS Code | Claude Code | 說明               |
| :------------------- | :-----: | :---------: | :----------------- |
| `.github/skills/`    |   ✅    |     ❌      | VS Code 專案層級   |
| `.agents/skills/`    |   ✅    |     ❌      | VS Code 專案層級   |
| `.claude/skills/`    |   ✅    |     ✅      | **最佳跨工具選擇** |
| `~/.copilot/skills/` |   ✅    |     ❌      | VS Code 使用者層級 |
| `~/.claude/skills/`  |   ✅    |     ✅      | 使用者層級跨工具   |

> 💡 若想讓 VS Code 與 Claude Code 都能讀取，建議將 Skills 放在 **`.claude/skills/`**。

---

## 📋 目錄

- [🤖 Custom Agents（自訂代理）](#-custom-agents自訂代理)
    - [什麼是 Custom Agent？](#什麼是-custom-agent)
    - [檔案位置](#1-檔案位置)
    - [Frontmatter 欄位說明](#2-frontmatter-欄位說明)
    - [Agent 範例](#3-agent-範例)
- [🛠️ Agent Skills（技能）](#️-agent-skills技能)
    - [什麼是 Agent Skill？](#什麼是-agent-skill)
    - [目錄結構](#1-目錄結構)
    - [SKILL.md 寫法](#2-skillmd-寫法)
    - [如何使用技能](#3-如何使用技能)
- [📂 本專案範例](#-本專案範例)
- [🎯 快速入門 Checklist](#-快速入門-checklist)
- [❓ 常見問題 FAQ](#-常見問題-faq)

---

## 🤖 Custom Agents（自訂代理）

### 什麼是 Custom Agent？

**Custom Agent** 是一組特定的指令與工具集合，讓你能將 Copilot 設定成具備特定角色的 AI 助理。

例如，你可以建立一個「安全審查代理」只使用唯讀工具，或建立一個「實作代理」擁有完整的編輯權限。切換 Agent 即可快速套用對應的工具與行為。

此外，透過 **Handoffs（交接）** 功能，Agent 之間可以串接成工作流程，例如：規劃完成後自動移交給實作代理。

### 1. 檔案位置

Custom Agent 定義在 `.agent.md` 檔案中，支援以下存放位置：

| 範圍             | 路徑                 |
| :--------------- | :------------------- |
| 工作區（標準）   | `.github/agents/`    |
| 工作區（Claude） | `.claude/agents/`    |
| 使用者個人       | `~/.copilot/agents/` |

> 💡 可透過 `chat.agentFilesLocations` 設定新增自訂搜尋路徑。

### 2. Frontmatter 欄位說明

```yaml
---
name: my-agent # [選填] 代理名稱，預設使用檔名
description: ... # [選填] 代理描述，顯示於 Chat 輸入框
argument-hint: ... # [選填] 提示使用者輸入的文字
tools: ['search', 'web'] # [選填] 此代理可使用的工具清單
model: GPT-4o (copilot) # [選填] 指定使用的 AI 模型
user-invocable: true # [選填] 是否顯示於代理下拉選單（預設 true）
handoffs: # [選填] 定義交接到下一個代理
    - label: 開始實作
      agent: implementation
      prompt: 依照上方計畫開始實作。
---
```

### 3. Agent 範例

```markdown
---
name: planning
description: 產生詳細的實作計畫
tools: ['search', 'web', 'codebase']
handoffs:
    - label: 開始實作
      agent: implementation
      prompt: 依照上方計畫開始實作。
---

# 規劃代理

你是一位資深解決方案架構師。在回答問題前，請先蒐集足夠的專案脈絡，
再產出清晰、具體、可執行的實作計畫。
```

---

## 🛠️ Agent Skills（技能）

### 什麼是 Agent Skill？

**Agent Skill** 是一組指令、腳本與資源的集合，讓 Copilot 能執行特定的專業任務。

與 Custom Instructions（自訂指令）不同，Skills 支援腳本、範例與其他資源，並遵循 [agentskills.io](https://agentskills.io/) 開放標準，可跨工具使用（VS Code、Copilot CLI、Copilot Coding Agent）。

**Skills 相較於 Custom Instructions 的優勢：**

| 項目     | Agent Skills                  | Custom Instructions   |
| :------- | :---------------------------- | :-------------------- |
| 用途     | 教導專業能力與工作流程        | 定義編碼標準與準則    |
| 可攜性   | 跨 VS Code、CLI、Coding Agent | VS Code 與 GitHub.com |
| 內容     | 指令、腳本、範例、資源        | 僅限指令              |
| 載入時機 | 按需載入（依相關性）          | 常駐套用              |
| 標準     | 開放標準 (agentskills.io)     | VS Code 專屬          |

### 1. 目錄結構

**一個 Skill = 一個資料夾**，資料夾名稱必須與 `SKILL.md` 中的 `name` 欄位一致。

Skills 支援以下存放位置（詳見上方[跨工具支援](#-跨工具支援)章節）：

| 範圍              | 路徑                                 | VS Code | Claude Code |
| :---------------- | :----------------------------------- | :-----: | :---------: |
| 專案（通用）      | `.claude/skills/`                    |   ✅    |     ✅      |
| 專案（VS Code）   | `.agents/skills/`、`.github/skills/` |   ✅    |     ❌      |
| 使用者（通用）    | `~/.claude/skills/`                  |   ✅    |     ✅      |
| 使用者（VS Code） | `~/.copilot/skills/`                 |   ✅    |     ❌      |

**完整目錄結構範例：**

```
.claude/                  # 推薦：VS Code + Claude Code 都能讀取
└── skills/
    └── my-skill-name/    # 資料夾名稱 = SKILL.md 中的 name 欄位
        ├── SKILL.md      # 🔴 必填：技能定義檔
        ├── references/   # 🟢 選填：靜態參考資料（如 API 文件）
        │   └── api-spec.md
        ├── assets/       # 🟢 選填：程式碼範本、靜態資源
        │   └── component.tsx
        └── scripts/      # 🟢 選填：執行腳本
            └── deploy.sh
```

### 2. `SKILL.md` 寫法

#### Frontmatter（必填）

```yaml
---
name: my-skill-name # 🔴 [必填] 技能唯一識別碼，小寫 kebab-case，需與資料夾名稱一致
description: ... # 🔴 [必填] 描述技能用途與觸發情境，最多 1024 字元
argument-hint: ... # 🟢 [選填] 作為 slash 指令時顯示的提示文字
user-invocable: true # 🟢 [選填] 是否顯示於 / 指令選單（預設 true）
disable-model-invocation: false # 🟢 [選填] 是否禁止 AI 自動載入（預設 false）
---
```

> **⚠️ 重點提醒：**
>
> `name` 必須與**資料夾名稱完全一致**，否則技能不會被載入！
>
> `description` 是 Copilot 判斷何時自動載入此技能的唯一依據，請清楚描述：
>
> 1. **什麼情況下**觸發此技能
> 2. **用來做什麼**

#### Body（內文）

Markdown 內文描述 Copilot 使用此技能時應遵循的步驟與規範。如有引用額外檔案，請使用相對路徑的 Markdown 連結：

```markdown
請參考 [測試範本](./templates/test-template.js) 來生成測試檔案。
```

### 3. 如何使用技能

技能可透過以下兩種方式觸發：

- **自動載入**：Copilot 依據對話內容與 `description` 相關性自動套用
- **Slash 指令**：在 Chat 輸入框輸入 `/` 可看到所有可用技能，直接選取即可

---

## 📂 本專案範例

本專案的 Skills 以**英文撰寫**（方便 AI 理解），並在 `中文版/` 資料夾提供對應的繁體中文版本。

Skills 存放於 **`.claude/skills/`**（VS Code 與 Claude Code 皆可讀取）。

### Skills 範例

| 資料夾                                         | 說明                                                                     |
| :--------------------------------------------- | :----------------------------------------------------------------------- |
| `.claude/skills/component-structure/`          | 建立元件或 UI 區塊時觸發，強制套用 Atomic Design 架構與檔案匯出規範      |
| `.claude/skills/file-naming-convention/`       | 建立或修改檔案時觸發，強制套用全域 kebab-case 命名規範                   |
| `.claude/skills/jsdoc-convention/`             | 撰寫或重構 TypeScript/JavaScript 程式碼時觸發，強制套用繁體中文 JSDoc    |
| `.claude/skills/reactjs-nextjs-patterns/`      | 撰寫 React 元件或 Next.js 頁面時觸發，強制套用最佳實踐與 App Router 規範 |
| `.claude/skills/traditional-chinese-language/` | 所有 AI 回應與提問一律使用繁體中文（台灣）                               |

---

## 🎯 快速入門 Checklist

### Step 1: 建立目錄結構

若只使用 VS Code，可使用 `.agents/skills/`（官方 Quickstart 預設）：

```bash
mkdir -p .agents/skills
```

若想讓 VS Code 與 Claude Code 都能讀取（**推薦，最大化相容性**）：

```bash
mkdir -p .claude/skills
```

### Step 2: 新增你的第一個 Skill

1. 建立 Skill 資料夾（資料夾名稱即為技能的 `name`）
2. 建立核心檔案 `SKILL.md`：

```markdown
---
name: my-first-skill
description: 當使用者詢問 XXX 時啟動，用於 YYY。
---

# My First Skill

## 執行步驟

1. 第一步做什麼
2. 第二步做什麼
```

### Step 3: （選填）新增 Custom Agent

在 `.github/agents/` 建立 `my-agent.agent.md`：

```markdown
---
name: my-agent
description: 專注於 XXX 任務的代理
tools: ['codebase', 'search']
---

# My Agent

你是一位專精於 XXX 的 AI 助理，請依照以下準則運作...
```

### Step 4: 測試

在 VS Code Chat 中切換至你的 Custom Agent，或輸入 `/` 查看可用技能，觀察是否正確套用！

---

## ❓ 常見問題 FAQ

### Q1: Custom Agent 跟 Agent Skill 有什麼差別？

| 項目 | Custom Agent                       | Agent Skill                      |
| ---- | ---------------------------------- | -------------------------------- |
| 性質 | 持久性角色 / 工具限制配置          | 按需載入的專業能力               |
| 用途 | 定義 AI 的角色、可用工具、模型偏好 | 賦予 AI 執行特定任務的能力與知識 |
| 格式 | 單一 `.agent.md` 檔案              | 一個資料夾 + `SKILL.md`          |
| 觸發 | 使用者手動切換代理                 | AI 依相關性自動載入，或 `/` 指令 |
| 範例 | 安全審查代理、規劃代理、實作代理   | 測試工作流、除錯步驟、部署腳本   |

### Q2: Agent Skills 只能在 VS Code 用嗎？

**不是**。Agent Skills 是 [agentskills.io](https://agentskills.io/) 開放標準，支援的工具包括：

- **Claude Code**：讀取 `.claude/skills/`
- **VS Code GitHub Copilot**：讀取 `.agents/skills/`、`.github/skills/`、`.claude/skills/`
- **Goose、JetBrains Junie、TRAE、Factory** 等多種工具

若想最大化相容性，建議將 Skills 放在 **`.claude/skills/`**（VS Code 與 Claude Code 都支援）。

> 💡 agentskills.io 官方 Quickstart 明確指出：「The same skill works in any compatible agent, **including Claude Code and OpenAI Codex**.」

**目前不支援** Agent Skills 標準的工具：Gemini CLI（有各自的 context loading 機制，但不支援 SKILL.md 自動發現格式）。

### Q3: 為什麼我的 Skill 沒有被觸發？

1. **檢查目錄路徑**：所使用的 AI 工具是否讀取該路徑？（參考上方跨工具支援表格）
2. **檢查 `name` 與資料夾名稱**：兩者必須完全一致（大小寫敏感）
3. **檢查 `description`**：是否清楚描述了觸發條件與用途？
4. **手動觸發**：在 Chat 輸入 `/` 並選取技能，確認是否出現在清單中
5. **查看診斷**（VS Code）：在 Chat 右鍵選 **Diagnostics** 可查看所有載入的技能與錯誤訊息

### Q4: 我可以有多少個 Skills？

沒有硬性限制。支援工具普遍採用**漸進式載入**，只有相關的技能才會被載入到 Context，因此安裝多個技能不會影響效能。

### Q5: 檔案可以用中文命名嗎？

**不建議**。`name` 欄位僅支援小寫英文與連字號（kebab-case），資料夾名稱需與其一致。

---

## 📝 附錄：專案結構總覽

```
.claude/
└── skills/                                       # 🧰 技能目錄（英文版，VS Code + Claude Code 皆可讀取）
    ├── component-structure/
    │   └── SKILL.md                              # Atomic Design 元件架構規範
    ├── file-naming-convention/
    │   └── SKILL.md                              # 全域 kebab-case 命名規範
    ├── jsdoc-convention/
    │   └── SKILL.md                              # Google Style 繁體中文 JSDoc
    ├── reactjs-nextjs-patterns/
    │   └── SKILL.md                              # React.js & Next.js 開發模式
    └── traditional-chinese-language/
        └── SKILL.md                              # AI 回應與提問一律使用繁體中文

中文版/
└── skills/                                       # 🧰 技能目錄（繁體中文版）
    ├── component-structure/
    │   └── SKILL.md
    ├── file-naming-convention/
    │   └── SKILL.md
    ├── jsdoc-convention/
    │   └── SKILL.md
    ├── reactjs-nextjs-patterns/
    │   └── SKILL.md
    └── traditional-chinese-language/
        └── SKILL.md
```

---

> 🎉 **配置完成後，就可以開始享受 Agent 帶來的高效開發體驗了！**
>
> 如有問題，歡迎查閱官方文件或參考本專案範例。
