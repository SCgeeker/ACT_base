---
name: annotation-card-review
description: >
  生成 Card Review (Narrative Draft) 從匯入的原子卡片，協助理解論文結構並為 Connection Gear 準備高質量起點。
  使用時機：匯入論文後、需要理解論文整體論述、準備撰寫 Connection Gear、想快速掌握論文貢獻與卡片分佈。
  觸發詞：「生成 Card Review」「起草敘事」「review cards」「Card Review」「整理卡片」「看這篇論文」「論文卡片」。
  只要使用者匯入新論文或想理解 annotation 卡片，就應使用此 skill 而非直接瀏覽卡片。
argument-hint: <citekey> [<kb_output_path>] [--style experimental|methodological|review]
allowed-tools: Read, Glob, Grep, Write, Edit
---

# Card Review (Narrative Draft)

將 zettel_index.md 中的原子卡片編織成流暢的學術敘事，為 Connection Gear 撰寫提供高質量起點。

## 品質分工

| 角色 | 貢獻比例 | 職責 |
|------|---------|------|
| **AI** | 70-90% | 解析卡片結構、生成流暢敘事、添加 Potential Gear Hints |
| **Human** | 10-30% | 精煉語言、調整結構、標記優先 Gears |

## 執行流程

### Step 1: 解析輸入與驗證卡片

解析 arguments：
- 第一個 token = `<citekey>`
- 若有第二個 token 且為路徑 = `<kb_output_path>`（Marp slides，可選）
- `--style` flag 指定風格（可選）

執行驗證：

```
1. 讀取：ACT/0️⃣Annotation/{citekey}/{citekey}.md
   - 從「# 📚 卡片清單」區段取得卡片列表
   - 讀取 frontmatter card_count

2. 計算 cards/ 資料夾實際卡片數：
   - Glob: ACT/0️⃣Annotation/{citekey}/cards/{citekey}-*.md
   - available_count = 實際檔案數

3. 驗證並回報：
   - available_count vs. frontmatter card_count 是否一致
   - 若不一致，以 available_count 為準並標記差異

4. 若有 <kb_output_path>，讀取作為內容補充來源
```

> **注意**：本 vault 不使用 `zettel_index.md`。卡片清單在主 note 的「📚 卡片清單」區段。

### Step 2: 識別論文風格

若使用者未指定 `--style`，根據以下特徵自動判斷：

| 風格 | 特徵關鍵詞 |
|------|-----------|
| **experimental** | 參與者、實驗設計、統計分析、假說驗證 |
| **methodological** | 模型架構、計算方法、效率評估、消融實驗 |
| **review** | 文獻回顧、理論整合、框架比較、研究缺口 |

### Step 3: 套用模板

根據風格載入對應模板：
- 實驗型：[templates/experimental.md](templates/experimental.md)
- 方法論型：[templates/methodological.md](templates/methodological.md)
- 綜述型：[templates/review.md](templates/review.md)

### Step 4: 生成 Narrative Draft

**結構要求**：
- 按邏輯順序組織（背景 → 方法 → 結果 → 討論）
- 每個區塊 2-4 段落，段落流暢連貫
- 區塊之間有清晰的過渡

**引用要求**：
- 每個關鍵概念都鏈接到卡片：`[[cards/Author-Year-XXX|display text]]`
- 第三人稱學術風格：`The authors proposed...`, `The study found...`
- 避免列表式摘要，使用完整句子

**Gear Hints 要求**：
- 每個區塊末尾添加 `**→ Potential Gear**`
- 識別理論張力、方法論創新、未解決問題

### Step 5: 輸出

將 Narrative Draft 寫入：
```
ACT/0️⃣Annotation/{citekey}/{citekey}.md
```
插入位置：概念網絡圖（mermaid）之後、Connection Gear 之前

## 輸出格式範例

```markdown
## Collaborated Annotations

### 研究背景與理論框架

The authors situate their work within the debate on [[cards/Author-Year-001|embodied cognition]],
challenging the traditional view that [[cards/Author-Year-002|conceptual representations]]
are amodal. Building on prior work by Barsalou (1999), they propose...

**→ Potential Gear**: 傳統命題表徵與感知符號系統之間的理論張力

### 研究設計與方法

The study employed a [[cards/Author-Year-005|similarity judgment task]] with
N=120 participants. The experimental manipulation involved...

**→ Potential Gear**: 隱性 vs 顯性詞綴效果的測量方法創新
```

## 品質檢查清單

- [ ] 所有 available_count 張卡片至少被引用一次
- [ ] Potential Gear Hints 數量 ≥ 3
- [ ] 無列表式摘要（全為流暢段落）
- [ ] 連結語法正確：`[[{citekey}-XXX.md|text]]`（無 `cards/` 前綴，保留 `.md`）
- [ ] 學術第三人稱語氣

## 下一步

完成 Card Review 後，建議：
1. **人類修訂**（10-30%）：調整語言、補充連接、標記優先 Gears
2. **啟動 Gear Coaching**：`/annotation-gear-coaching {citekey}` 進入 Phase 1

## 相關資源

- [Connection Gear Template](Templates/Connection%20Gear%20Template.md) - Gear 模板
- [ACT space](ACT/ACT%20space.md) - ACT 儀表板
