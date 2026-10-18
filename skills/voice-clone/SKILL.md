---
name: voice-clone
description: 使用 CK（建國）已錄製的聲音（CK_Voice）以 VoxCPM2 進行語音複製／克隆（TTS），在 Apple Silicon 以 MPS 加速。使用者提到「用建國的聲音」「用 CK 的聲音」「CK voice」「克隆／複製我的聲音」「用我的聲音唸／說／朗讀」「生成我的語音」時載入。僅限語音合成，不支援真正唱歌。
license: MIT
---

# CK Voice 語音克隆（VoxCPM2 + MPS）

> 寫給 AI agent 執行。目標：把使用者提供的文字，用 CK 的克隆聲音生成 wav。

## 固定環境（本機）

| 項目 | 路徑 |
|---|---|
| 專案目錄 | `/Users/ckliao/Antigravity/Projects/Voice_Clone` |
| Python | `/Users/ckliao/Antigravity/Projects/Voice_Clone/.venv/bin/python` |
| 預設聲音 | `CK_Voice`（`voices/CK_Voice/ref_voice.wav` + `prompt.txt`） |
| 預設輸出目錄 | `/Users/ckliao/Antigravity/Projects/Voice_Clone/output/` |

## 執行步驟

1. **前置檢查（唯讀）**：確認 Python 與 `voices/<聲音>/ref_voice.wav`、`prompt.txt` 存在。缺任一項就停止，回報並請 CK 先錄音（`webui_record.py` 或 `record.py`），不得自行編造參考音。
2. **整理文字**：保留使用者原文；詩詞、歌詞可用標點斷句。使用者說的詩名／人名若有誤，生成前先更正並於回覆中說明。
3. **生成**（一律用參數陣列式呼叫，文字不要拼進 shell 字串；含引號或特殊字元時改用 `--file` 讀文字檔）：

```bash
PYTORCH_ENABLE_MPS_FALLBACK=1 /Users/ckliao/Antigravity/Projects/Voice_Clone/.venv/bin/python \
  /Users/ckliao/Antigravity/Projects/Voice_Clone/clone.py "要生成的文字" \
  --voice CK_Voice --device mps \
  --output /Users/ckliao/Antigravity/Projects/Voice_Clone/output/<有意義的檔名>.wav
```

- 輸出路徑務必用**絕對路徑**（`clone.py` 預設為相對路徑，在其他目錄執行會寫錯位置）。
- 檔名不要覆蓋既有檔案（例如 `cloned_voice.wav`），先確認再寫。
- 若 MPS 出錯，改用 `--device cpu` 重試，並告知 CK 已降級。
- 長文：分段（每段約 100 字內）逐段生成，再告知各檔位置，避免單次過長。
- 使用者指定其他聲音：把 `--voice` 換成 `ls voices/` 中存在的名稱。

4. **回報**：附輸出檔連結、裝置、語音長度、耗時（RTF）。明說「未實際聆聽音質與咬字，請自行確認」。

## 實測基準（Apple Silicon，MPS）

- 約 6–7 秒語音需 10–12 秒生成（RTF 約 1.4–1.9）。
- 首次執行會下載約 4.7GB 模型；之後使用快取。

## 限制與風險

- VoxCPM2 為 TTS，**不會依旋律唱歌**；使用者要求「唱」時，先說明只能有節奏地朗讀，真正唱歌需歌聲轉換工具。
- MPS 非官方支援（官方僅 CUDA），可能有未支援運算。
- **聲音屬生物特徵個資**：不得上傳、外傳或提交 `voices/` 內容到版控；不得用於冒充他人、詐騙或未經同意之第三方聲音克隆。
- 不得將任何 API Key、Token 寫入此 skill 或輸出檔案。
- 若使用者提出克隆**其他人**的聲音，需先確認已取得本人同意。
