---
name: start-work
description: Use when CK says 開工、開始工作、我來了、上次做到哪、繼續、接續工作或需要在另一台電腦恢復專案。
---

# 開工：跨裝置工作恢復

以來源版 `startup` 的三層架構恢復工作：L1 本地交接、L2 Git 狀態、L3 Obsidian 詳細脈絡。開工只讀、只報告。

## L1 本地交接（必做）

1. 找到 Git 根目錄或目前專案根目錄，讀取所有適用的 `AGENTS.md`。
2. 讀取 `.agent/HANDOFF.md`；舊專案若只有 `handoff.md`，可唯讀摘要並提議遷移，未經確認不得建立或改寫。
3. 比對交接檔 `branch`、`base_commit`、HEAD 與 `git status --short`。HEAD 若只有交接檔變更，可接受 `base_commit` 指向其父 commit。
4. 若交接資料含上次收工裝置或時間，與目前裝置／檔案時間比對；不一致時標示「可能來自另一台電腦，先確認同步」。

## L2 Git 與遠端（有 `.git` 才做）

- 回報目前分支、最新 commit、未提交變更與遠端設定。
- 需要檢查遠端時，先取得 CK 同意再執行 `git fetch`；30 分鐘內已 fetch 可略過。
- 絕不主動 `git pull`、切換分支、clean、commit、push 或修改檔案；不執行 reset。

## L3 Obsidian（條件式）

若 `AGENTS.md` 或交接檔有登記 Obsidian 路徑，只列出路徑。只有交接檔明確指向該筆記，或 CK 明確要求時才讀取。

## 回報格式

```text
📂 專案：<名稱>（L1／L2／L3）
📘 上次做到哪：<摘要>
🔧 本地 Git：<乾淨／未提交變更／非 Git>
🌐 遠端：<未檢查／最新／需 fetch 後確認>
🧠 Obsidian：<路徑或未設定>
⚠️ 風險：<分支、基準、同步或機密警示>
➡️ 建議下一步：<1–3 項>
```

停止並等待 CK 選擇下一步。交接檔格式請讀取 [交接契約](references/handoff-contract.md)。
