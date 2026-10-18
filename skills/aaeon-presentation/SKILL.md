---
name: aaeon-presentation
description: AAEON（研揚科技）標準 9 頁功能簡報製作與自動化投影片生成技能。適用於研揚硬體架構評估、技術方案權衡（Trade-off）、技術支柱分析（Core Pillars）、風險矩陣（Risk Matrix）、專案時程里程碑（Schedule & Milestones）等專業簡報製作與 PPTX 檔案生成。
license: MIT
---

# AAEON 簡報製作模板技能 (AAEON Presentation Skill)

本技能定義了 AAEON（研揚科技）標準 9 頁功能性與技術架構簡報的內容架構規範、色彩語意、排版邏輯與自動化生成工具鏈。

---

## 1. 核心定位與適用情境

當使用者需要：
1. **規劃 AAEON 簡報架構**：針對硬體架構、技術評估、專案審查或產品發布，產出符合研揚標準結構的 Markdown 內容。
2. **自動生成實體 PPTX 檔案**：將技術大綱、規格數據或結構化 JSON 直接套版寫入 `AAEON_Template_v2.pptx`。
3. **優化與修訂簡報文案**：依據 9 大經典版型（Archetypes）重構既有投影片邏輯。

---

## 2. AAEON 9 大標準版型結構 (Slide Archetypes)

| 頁碼 | 版型名稱 (Archetype) | 核心用途與結構 |
| :--- | :--- | :--- |
| **01** | **封面頁 (Cover)** | `[簡報主標題]`、`[簡報副標題 / 專案名稱]`、`[發表單位 / 日期 / Presenter]` |
| **02** | **大綱架構 (Agenda & Framework)** | 5 大主題方塊，各包含「編號與章節標題」＋「• 核心摘要與預期效益說明」 |
| **03** | **章節轉場 (Section Divider)** | `01 / [章節主標題]`、`[Chapter English Title]`、`[章節核心範圍或技術摘要]` |
| **04** | **核心摘要 (Executive Summary)** | **雙卡片單欄佈局**：<br>• 上卡片：`【核心結論（Executive Takeaway）】`（1~2 句關鍵決策、最佳方案與量化效益）<br>• 下卡片：`關鍵架構分析重點（Key Architectural Pillars）`（3~4 點核心重點深入） |
| **05** | **技術權衡 (Technical Trade-off)** | **左右對比卡片**（Option A vs Option B）：<br>包含「方案特徵」、「優點 (Pros)」、「缺點 (Cons)」、「BOM 成本衝擊」、「設計規範要求」與「建議評估（標註推薦）」 |
| **06** | **三大技術支柱 (Core Technical Pillars)** | **三欄並列卡片**（如：電源/電氣、高速訊號 SI、散熱機構）：<br>每欄包含「中英文支柱名稱」＋ 3 點具體技術要點、規範數據與驗證標準 |
| **07** | **風險矩陣 (Risk Matrix & Mitigation)** | **四象限分析卡片**：<br>1. `【高衝擊 / 高機率】關鍵技術風險`<br>2. `【高衝擊 / 低機率】平台相容風險`<br>3. `【低衝擊 / 高機率】機構公差風險`<br>4. `【低衝擊 / 低機率】常規物料交期`<br>各附「風險點描述」與「具體因應對策」 |
| **08** | **時程里程碑 (Schedule & Milestones)** | **四階段推進流程卡片**：<br>• `Phase 1：Q1 (Architecture & Spec Freeze)`<br>• `Phase 2：Q2 (Schematic & PCB Layout)`<br>• `Phase 3：Q3 (EVT / DVT Validation)`<br>• `Phase 4：Q4 (PVT & Mass Production)`<br>各附 3 項關鍵里程碑工作 |
| **09** | **結尾頁 (Thank You & Q&A)** | `Thank You`、`Q&A 與討論交流`、`研揚科技 AAEON Technology Inc.  |  研發中心` |

---

## 3. 視覺語意與撰寫原則

1. **結論先行（Bottom-Line Upfront）**：Slide 04 的 Takeaway 必須直接點出結論與推薦方案，不拐彎抹角。
2. **量化與專業術語**：技術細節必須精確標示電氣/訊號/溫度數據（如 `PCIe Gen5`、`DDR5 5600MT/s`、`-40°C~85°C`、`85Ω ±10%`），術語首次出現採用「中文（English）」。
3. **高對比與視覺平衡**：文字精簡條列化，避免大段落文字擠壓。

---

## 4. 自動化生成 PPTX 指南 (Automation Toolchain)

本技能隨附 Python 自動化填版工具，位於 `scripts/generate_presentation.py`。

### 執行方式
```bash
python "C:\Users\GL76\.gemini\config\skills\aaeon-presentation\scripts\generate_presentation.py" \
    --input "path/to/payload.json" \
    --output "path/to/output.pptx" \
    [--template "optional/custom/template.pptx"]
```

### 範例 Payload 結構
可參考 `scripts/sample_payload.json`，格式如下：
```json
{
  "slides": {
    "1": { "title": "主標題", "subtitle": "副標題", "presenter": "單位名稱" },
    "2": { "title": "大綱標題", "items": [{ "heading": "01 主題", "description": "• 說明" }] },
    "3": { "chapter_number": "01", "title": "章節名稱", "subtitle_en": "English", "summary": "摘要" },
    "4": { "title": "標題", "takeaway": "核心結論說明", "pillars": ["重點 1", "重點 2"] },
    "5": {
      "title": "方案比較",
      "option_a": { "header": "方案 A", "subtitle": "特徵", "pros": "優點", "cons": "缺點", "cost": "成本", "spec": "規範", "recommendation": "建議" },
      "option_b": { "header": "方案 B - 建議方案", "subtitle": "特徵", "pros": "優點", "cons": "缺點", "cost": "成本", "spec": "規範", "recommendation": "【推薦】" }
    },
    "6": {
      "title": "三大支柱",
      "pillars": [
        { "title_zh": "支柱一", "title_en": "Pillar 1", "points": ["【要點 A】說明", "【要點 B】說明"] }
      ]
    },
    "7": {
      "title": "風險矩陣",
      "risks": [
        { "header": "【高衝擊 / 高機率】關鍵技術風險", "risk": "風險描述", "mitigation": "• 對策一 • 對策二" }
      ]
    },
    "8": {
      "title": "時程規劃",
      "phases": [
        { "phase": "Phase 1：Q1 2026", "title_zh": "架構凍結", "title_en": "Spec Freeze", "tasks": ["任務 1", "任務 2"] }
      ]
    },
    "9": { "main_text": "Thank You", "sub_text": "Q&A 與討論交流", "company": "研揚科技 AAEON Technology Inc." }
  }
}
```

---

## 5. 資源路徑參考
- **標準空白模板**：`resources/AAEON_Template_v2.pptx`
- **雲端同步模板備份**：`G:\我的雲端硬碟\AAEON\簡報製作\AAEON_功能簡報空白模板_Template_v2.pptx`
- **版型細節對照手冊**：`references/layout_spec.md`