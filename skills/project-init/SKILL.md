---
name: project-init
description: Use when CK says 初始化專案、專案初始化、開新專案、建立專案藍圖、幫我 init 專案或需要建立跨裝置交接基礎。
---

# 專案初始化：跨裝置三層基礎

以來源版 `project-init` 的三層架構建立新專案；先盤點、再預覽、確認後才寫入。

## 層級偵測

| 層級 | 內容 | 啟用條件 |
|---|---|---|
| L1 | `AGENTS.md`、`.agent/HANDOFF.md` | 永遠可建立 |
| L2 | Git 與私有 GitHub repo | Git／GitHub 可用且 CK 明確確認 |
| L3 | Obsidian 專案筆記 | Obsidian 可用且 CK 明確確認 |

## 流程

1. 唯讀掃描目前目錄、既有 `AGENTS.md`、`.agent/HANDOFF.md`、Git 與 Obsidian 可用性；若同名檔案存在，停止並提出合併／覆寫差異，未經確認不得覆寫。
2. 確認專案名稱、一句話目標、重要時程；沒有資料時寫「未提供」，不得編造。
3. 先顯示 L1 預覽，使用 [AGENTS 範本](templates/AGENTS.template.md) 與 [交接範本](templates/handoff.template.md)。
4. CK 確認後建立 L1。
5. 若要 L2，先顯示 `.gitignore`、初始 commit 訊息與私有 repo 名稱；CK 分別確認 git init、commit、push／建 repo 後才執行。不得預設建立 public repo。
6. 若要 L3，先顯示將建立的 Obsidian 筆記位置與內容摘要；CK 確認後才寫入。

## 安全邊界

- 不自行覆寫既有檔案、建立 repo、commit、push、建立 PR 或寫入 Obsidian。
- `.env`、金鑰、憑證、Cookie、Token、模型權重與用途不明檔案不得納入 Git。
- 專案完成 L1 後，日常恢復使用 `start-work`，交接使用 `end-work`。
