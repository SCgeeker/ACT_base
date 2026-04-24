---
name: annotation-monitor
description: >
  Vault Lint 操作：掃描所有 Annotations 的完成狀態，分類舊格式孤兒筆記，識別孤兒卡片與概念孤兒，輸出 Lint Action Queue 並路由到正確修復指令。
  使用時機：定期工作規劃、想知道哪些論文還沒寫 Gear、識別舊格式積壓、識別概念缺口、每週 vault 健康檢視。
  觸發詞：「掃描」「monitor」「未完成 Gear」「狀態報告」「哪些還沒寫 Gear」「工作清單」「待處理論文」「積壓」「lint」「孤兒筆記」「舊格式」「orphan」。
  定期規劃或工作開始前，應主動建議使用此 skill 了解 vault 狀態。
user-invocable: true
allowed-tools: Read, Glob, Grep, Bash
---

# Annotation Monitor — Vault Lint Operation

掃描 vault 中所有 Annotation 的完成狀態，分類問題，輸出可直接執行的 Lint Action Queue。

---

## 監控目標（4 類）

| 類別 | 識別方式 | 輸出路由 |
|------|---------|---------|
| **Gear 未完成** | `geared: false` 或 `geared: []` | `/annotation-gear-coaching` |
| **舊格式孤兒** | `@Author-Year.md` 格式 | 分 Type M/G/F（見下方） |
| **孤兒卡片** | `cards/` 存在但主 note `geared: false` 且無 Connection 反向連結 | `/annotation-card-review` |
| **概念孤兒** | 同一詞彙出現於 3+ 個 Gear 內文，但無對應 Connection note | 建議建立 Connection stub |

---

## 舊格式孤兒分類矩陣（Orphan Classification Matrix）

舊格式 `@Author-Year.md` 依內容狀態分三類，路由到不同修復路徑：

| 類型 | 判斷條件 | 處理路徑 |
|------|---------|---------|
| **Type M**（Migrate only） | 有 Gear 內容 + 有敘事段落 | `/annotation-migrate` → 完成 |
| **Type G**（Migrate + Gear） | 有敘事段落，但 `geared: false` | `/annotation-migrate` → `/annotation-gear-coaching` |
| **Type F**（Fresh decision） | 幾乎空白 / 只有 frontmatter | 決策：有 PDF → 重新 import；無 PDF → recycle |

---

## 執行步驟

### Step 1: 掃描所有 Annotations

```bash
# 新格式（資料夾結構）
Glob: ACT/0️⃣Annotation/*/

# 舊格式
Glob: ACT/0️⃣Annotation/@*.md
```

### Step 2: Vault Health Dashboard（CLI）

```bash
# 孤兒筆記：無反向連結
obsidian vault=ACT_Base orphans total

# 死端筆記：無外向連結
obsidian vault=ACT_Base deadends total

# 未解析連結
obsidian vault=ACT_Base unresolved total

# ACT 檔案計數
obsidian vault=ACT_Base files folder=ACT total
```

### Step 3: 分類舊格式孤兒

對每個 `@Author-Year.md`：
1. 讀取 frontmatter：`geared` 欄位
2. 掃描 body：是否有 `## Connection Gear` 段落（Type M）；是否有敘事段落（>3 行非標題內容）
3. 若兩者皆無 → Type F

### Step 4: 識別孤兒卡片

```bash
# 有 cards/ 資料夾但 geared: false 的新格式 annotation
Glob: ACT/0️⃣Annotation/*/cards/
```
讀取對應主 note，確認 `geared` 狀態與是否有 Connection 反向連結（`conn:` 欄位非空）。

### Step 5: 識別概念孤兒

```bash
# 取出所有 Connection Gear 段落的關鍵詞
Grep: pattern="## Connection Gear" context=50 in ACT/0️⃣Annotation/**/*.md
```

跨 Gear 統計高頻詞（3+ 次出現），與現有 Connection notes 標題比對：
```bash
Glob: ACT/1️⃣Conn/*.md
```
若高頻詞無對應 Connection note 標題 → 標記為「概念孤兒」。

### Step 6: 評估優先級

- 與活躍 Connections 相關 → 高優先
- 出現在 `orphans` 清單 → 高優先
- 舊格式 Type G → 中優先
- 舊格式 Type M → 中優先（快速可完成）
- 舊格式 Type F → 低優先（需要人類決策）

---

## 輸出格式

```markdown
## Annotation Lint Report

**掃描時間**：[日期時間]
**總計 Annotations**：[N] 篇（新格式 [A] + 舊格式 [B]）

---

### Vault Health Dashboard

| 指標 | 數量 | 說明 |
|------|------|------|
| 孤兒筆記 | [X] | 無反向連結 — 可能被遺忘 |
| 死端筆記 | [Y] | 無外向連結 — 可能缺少 Gear 或 wikilinks |
| 未解析連結 | [Z] | 指向不存在的筆記 — 需要修復 |
| ACT 檔案總數 | [W] | ACT 資料夾內所有檔案 |

---

### Lint Action Queue

優先級排序，每筆直接對應可執行指令：

| # | Annotation | 類型 | 問題 | 執行指令 |
|---|------------|------|------|---------|
| 1 | [[Barsalou-1999]] | 新格式 | Gear 未完成，有 cards | `/annotation-gear-coaching Barsalou-1999` |
| 2 | @Rodriguez-2023 | 舊 Type M | 有 Gear，需遷移格式 | `/annotation-migrate Rodriguez-2023` |
| 3 | @Smith-2020 | 舊 Type G | 有敘事，無 Gear | `/annotation-migrate Smith-2020` → `/annotation-gear-coaching Smith-2020` |
| 4 | @Jones-2019 | 舊 Type F | 幾乎空白，有 PDF | 重新 import via QuickAdd → `/annotation-card-review Jones-2019` |

---

### 概念孤兒（Concept Orphans）

同一詞彙出現於 3+ 個 Gear 但無對應 Connection note：

| 概念詞彙 | 出現次數 | 出現於 | 建議動作 |
|---------|---------|-------|---------|
| [概念] | [N] 次 | [[A]], [[B]], [[C]] | 建立 `🔗[概念] Connection` stub |

---

### 孤兒卡片（Orphan Cards）

有 cards/ 但 geared: false 且無 Connection 反向連結：

| Annotation | 卡片數 | 建議動作 |
|------------|-------|---------|
| [[Friedrich-2025]] | 20 | `/annotation-card-review Friedrich-2025` → `/annotation-gear-coaching Friedrich-2025` |

---

### 舊格式摘要

| 類型 | 數量 | 總計 |
|------|------|------|
| Type M（只需遷移） | [X] 篇 | |
| Type G（遷移 + Gear） | [Y] 篇 | |
| Type F（需人類決策） | [Z] 篇 | [X+Y+Z] 篇 |
```

---

## 自動觸發（可選）

此 skill 可在以下情境自動建議：
- 使用者開始新工作階段時
- Connection note 需要更多來源時
- 定期週報檢視時

---

## 下一步路由

根據 Lint Action Queue：
- `/annotation-migrate {citekey}` — 遷移舊格式
- `/annotation-card-review {citekey}` — 處理有卡片的孤兒
- `/annotation-gear-coaching {citekey}` — 撰寫 Gear
- `/connection-gear-aggregate` — 處理概念孤兒，確認 Connection 機會
- QuickAdd → Import Zettel — Type F 有 PDF 者重新 import
