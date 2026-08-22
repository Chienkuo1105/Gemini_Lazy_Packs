---
name: end-work
description: Use when CK says 收工、結束了、下班、準備換電腦、同步、先到這裡、建立交接或需要保存跨裝置工作狀態。
---

# 收工：跨裝置安全交接

以來源版 `shutdown` 的三層架構保存工作：L1 本地交接、L2 GitHub、L3 Obsidian。所有寫入與同步均須分別取得 CK 明確確認。

## L1 本地交接（必做，但先預覽）

1. 讀取 `AGENTS.md`、目前分支、HEAD、工作樹差異、最近 commit 與既有 `.agent/HANDOFF.md`。
2. 只彙整可驗證內容：目前目標、已完成、決策、變更檔案、驗證、阻塞／風險、下一步與必要指令；未知內容標記「未驗證」。
3. 建立 HANDOFF v1 差異；`base_commit` 使用目前程式碼基準，`author_surface` 依執行端填入。可記錄收工時間與裝置資訊，但不得記錄機密。
4. 掃描 Token、密碼、私鑰與個資。命中時阻擋寫回。
5. 顯示完整差異及驗證結果。未經 CK 明確確認，不得寫檔、commit、push 或建立 PR。

## L2 GitHub（有 `.git` 且 CK 確認時）

- 先列出準備提交的已追蹤變更與 commit 草稿；未知或未追蹤檔案不得自動加入。
- 取得一次確認後才寫入交接檔；取得另一次確認後才 commit；取得再一次確認後才 push 或建立 PR。
- 受保護或預設分支使用 `agent/handoff-<timestamp>` 與 PR 流程。
- 遠端 MCP 寫入必須帶入 blob SHA 與 base commit；任一值變動即停止覆寫、重新讀取。

## L3 Obsidian（條件式）

若專案已登記 Obsidian 筆記且 CK 確認，將詳細決策、踩坑與同步狀態寫入筆記；交接檔只保留一頁內的必要摘要。Obsidian 不可用時，在交接預覽中標示「L3 未更新」。

## 回報格式

```text
✅／⚠️ L1 本地：<預覽／已確認寫入／阻擋原因>
✅／⚠️ L2 GitHub：<commit 草稿／已確認提交／未推送原因>
✅／⚠️ L3 Obsidian：<已更新／未設定／未更新原因>
下一步：<需要 CK 確認的確切動作>
```

交接檔格式請讀取 [交接契約](references/handoff-contract.md)。
