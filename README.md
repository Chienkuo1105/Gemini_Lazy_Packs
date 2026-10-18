# Gemini Lazy Packs (Antigravity AI Agent 懶人包)

本儲存庫整合了個人化 AI Agent（Jenny）全域自訂規則（AGENTS.md）與 33 個精選核心自訂 Skills，適用於 Antigravity / Gemini CLI 環境之快速備份與跨裝置部署。

---

## 📦 目錄結構

```text
Gemini_Lazy_Packs/
├── README.md               # 專案說明與部署指南
├── .gitignore              # 忽略暫存與機密檔案
├── rules/
│   └── GEMINI.md           # 脫敏後的全域行為準則與角色規範（AGENTS.md）
└── skills/                 # 自訂 Skills 集合（包含專案生命週期、質詢面談、TDD 工程實作、原理解說動畫等）
    ├── project-init/       # 專案初始化規範與藍圖建立
    ├── start-work/         # 開工與跨裝置工作恢復（唯讀檢查）
    ├── end-work/           # 收工與 HANDOFF v1 交接建立（含機密掃描）
    ├── ck-workflow/        # CK 專屬全生命週期工程工作流
    ├── motion-explainer/   # HyperFrames 原理解說動畫端到端製作
    ├── grill-me/           # 深度決策樹質詢面談
    ├── grilling/           # 質詢邏輯與架構推演
    └── ...                 # 其餘 TDD 實作、架構規格、聲音克隆與簡報生成技能
```

---

## 🚀 跨裝置部署 / 還原指南

### 1. 全域規則設定 (`rules/GEMINI.md`)
1. 將 `rules/GEMINI.md` 複製至新環境使用者目錄下的 `.gemini/`（例如 `C:\Users\<USER>\.gemini\GEMINI.md` 或 `~/.gemini/GEMINI.md`）。
2. 將檔案中的變數替換為個人環境設定：
   - `{{USER_NICKNAME}}`：您的稱呼／暱稱（如 `CK`）。
   - `{{YOUR_NAME}}`：手寫簽名名稱。
   - `{{OBSIDIAN_VAULT_PATH}}`：Obsidian 知識庫路徑（如 `D:\Obsidian\Database\知識庫`）。
   - `{{AI_GUIDE_PATH}}`：AI 工作站規範手冊路徑。

### 2. 自訂 Skills 部署 (`skills/`)
將 `skills/` 目錄內的所有子資料夾複製至本機技能目錄：
* **Windows**：`C:\Users\<USER>\.gemini\config\skills\`
* **macOS / Linux**：`~/.gemini/config/skills/`

---

## 🔒 機密與安全規範
* 本儲存庫為 **Private（私有）**。
* 所有全域規則均已進行脫敏處理，未包含個人敏感金鑰（API Keys）、Token、密碼或絕對私有路徑。
* 跨裝置同步時請遵守三層交接原則（L1 本地 / L2 Git / L3 知識庫），嚴禁將敏感憑證提交至任何儲存庫。