# Gemini CLI 指令清單 (中英文對照)

這是一份 Gemini CLI 可用指令的對照表，幫助您快速了解每個指令的功能。

## 1. 斜線指令 (Slash Commands `/`)
這些指令用於控制 CLI 本身的功能。

| 指令 | 功能說明 (中文) | Description (English) |
| :--- | :--- | :--- |
| `/help` (或 `/?`) | 顯示此說明資訊 | Displays help information. |
| `/about` | 顯示版本資訊 | Shows version information. |
| `/auth` | 更改身分驗證方式 | Opens a dialog to change the authentication method. |
| `/bug [標題]` | 提交關於 Gemini CLI 的問題回報 | Files an issue about Gemini CLI. |
| `/chat` | 管理對話存檔 (save, list, resume, delete, share) | Manages conversation history checkpoints. |
| `/clear` | 清除終端機螢幕 | Clears the terminal screen. |
| `/compress` | 將目前的對話內容壓縮成摘要以節省空間 | Replaces the chat context with a summary. |
| `/copy` | 複製最後一次的 AI 輸出內容 | Copies the last output to the clipboard. |
| `/directory` (或 `/dir`) | 管理工作區目錄 (add, show) | Manages workspace directories. |
| `/docs` | 在瀏覽器中開啟官方文件 | Opens Gemini CLI documentation in the browser. |
| `/editor` | 選擇偏好的編輯器 | Opens a dialog for selecting supported editors. |
| `/extensions` | 列出目前啟用的擴充功能 | Lists all active extensions. |
| `/hooks` | 管理行為攔截與自定義功能 | Manages CLI behavior hooks. |
| `/ide` | 管理 IDE (如 VS Code) 的整合功能 | Manages IDE integration. |
| `/init` | 初始化目前目錄，產生 `GEMINI.md` | Analyzes directory to generate `GEMINI.md`. |
| `/introspect` | 顯示偵錯資訊 | Provides debugging information. |
| `/mcp` | 管理 Model Context Protocol 伺服器 | Manages MCP servers and tools. |
| `/memory` | 管理 AI 的長期記憶與背景知識 | Manages AI's instructional context. |
| `/model` | 切換使用的 Gemini 模型 | Opens a dialog to choose your Gemini model. |
| `/policies` | 管理政策設定 | Manages policies. |
| `/privacy` | 查看隱私權政策與數據收集設定 | Displays Privacy Notice and consent. |
| `/quit` (或 `/exit`) | 退出 Gemini CLI | Exits Gemini CLI. |
| `/restore` | 將檔案還原到執行指令前的狀態 | Restores files to a previous state. |
| `/rewind` | 倒退回之前的對話進度 | Navigates backward through conversation. |
| `/resume` | 瀏覽並恢復先前的對話紀錄 | Browses and resumes previous sessions. |
| `/settings` | 開啟設定界面修改 CLI 設定 | Opens the settings editor. |
| `/shells` | 切換顯示背景執行的 Shell 視窗 | Toggles the background shells view. |
| `/setup-github` | 設定 GitHub 自動化功能 | Sets up GitHub Actions. |
| `/skills` | 管理代理人技能 (Skills) | Manages Agent Skills. |
| `/stats` | 顯示目前對話的詳細統計數據 (如 Token 使用量) | Displays detailed session statistics. |
| `/terminal-setup` | 設定終端機快捷鍵 | Configures terminal keybindings. |
| `/theme` | 更改視覺主題 (顏色等) | Opens a dialog to change the visual theme. |
| `/tools` | 顯示目前可用的工具清單 | Displays a list of available tools. |
| `/vim` | 切換輸入框的 Vim 編輯模式 | Toggles vim mode for input area. |

## 2. At 指令 (At Commands `@`)
用於在提問時快速加入檔案內容。

| 指令 | 功能說明 (中文) | Description (English) |
| :--- | :--- | :--- |
| `@<路徑>` | 將指定的檔案或資料夾內容加入對話背景 | Injects file or directory content into the prompt. |
| `@` | 單獨使用時，直接將輸入傳給模型 (不觸發特殊處理) | Passes the query as-is to the model. |

## 3. Shell 指令 (Shell Commands `!`)
用於直接執行電腦系統的指令。

| 指令 | 功能說明 (中文) | Description (English) |
| :--- | :--- | :--- |
| `!<指令>` | 執行指定的系統指令 (例如 `!ls` 或 `!pwd`) | Executes the specified shell command. |
| `!` | 切換「Shell 模式」，之後輸入的都會被當作系統指令 | Toggles shell mode. |

## 4. 快捷鍵 (Shortcuts)
| 按鍵 | 功能說明 (中文) | Description (English) |
| :--- | :--- | :--- |
| `Cmd + Z` / `Alt + Z` | 復原輸入 (Undo) | Undo text manipulation. |
| `Shift + Cmd + Z` | 取消復原 (Redo) | Redo text manipulation. |
