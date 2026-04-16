---
name: connection-query
description: >
  Query the ACT vault (Annotations, Connections, Thoughts) with a research question and synthesize a grounded answer from existing note content only.
  使用時機：想知道 vault 現有內容對某個研究問題的立場、想跨筆記整合已有洞見、想確認某個論點有哪些 Annotation/Thought 支撐、想找出 vault 的知識缺口。
  觸發詞：「vault 怎麼說」「現有文獻支持什麼」「這個問題有沒有答案」「哪些 Annotations 談到」「哪些 Thoughts 相關」「知識缺口在哪裡」「query the vault」「search across notes」「what does the vault say about」「vault-level query」「cross-note synthesis」。
  完成後可選擇將答案歸檔回 vault：作為新 Connection 的 stub 或現有 Connection 的 section，或作為 Thought note candidate。
argument-hint: "<research question>" [--scope annotations|connections|thoughts|all] [--file-back connection|thought|none]
allowed-tools: Read, Glob, Grep, Bash
user-invocable: true
reusable: true
---

# Connection Query Skill

針對使用者的研究問題，搜尋並綜合 ACT vault 內已有的 Annotation、Connection、Thought 內容，輸出有出處的結構化答案，並可選擇歸檔回 vault。

---

## Purpose（目的）

實作 Karpathy-style Query 操作：

1. **接收研究問題**（Read the Question）
   - 接受自由格式的研究問題，不限格式
   - 支援聚焦範圍：僅查 Annotations、僅查 Connections+Thoughts、或全查

2. **識別相關內容**（Locate Relevant Content）
   - 跨 Annotation Gears、Connection sections、Thought notes 搜尋
   - 辨識直接相關、間接相關、以及彼此矛盾的內容

3. **合成有出處的答案**（Synthesize Grounded Answer）
   - 所有主張必須連結到具體來源（THE FIRST RULE）
   - 禁止幻覺：只整合 vault 現有內容，不補充外部知識
   - 標示來源類型（Annotation Gear / Connection section / Thought note）

4. **標記缺口**（Flag Gaps）
   - 找出問題觸及但 vault 中尚無充分回應的面向
   - 區分：(a) vault 完全未涵蓋、(b) vault 有線索但未展開、(c) vault 存在矛盾但未解決

5. **提供歸檔選項**（Offer to File Back）
   - 合成答案可選擇歸檔回 vault
   - 選項：新 Connection stub、現有 Connection 新 section、Thought note candidate

---

## Input（輸入）

### 基本模式（自由問句）
```
/connection-query "What do the annotations say about classifier typology and mental simulation?"
```

### 指定搜尋範圍
```
/connection-query "How is the C/M distinction operationalized?" --scope annotations
/connection-query "What Thoughts have emerged about individuation?" --scope thoughts
/connection-query "What is the vault's current position on embodied simulation?" --scope all
```

### 搜尋範圍說明
- `--scope annotations`：只搜尋 `ACT/0️⃣Annotation/` 的 Connection Gear 段落
- `--scope connections`：只搜尋 `ACT/1️⃣Conn/` 的 Connection notes
- `--scope thoughts`：只搜尋 `ACT/2️⃣Thought/` 的 Thought notes
- `--scope all`（預設）：三層全搜

### 歸檔選項
```
/connection-query "..." --file-back connection   # 輸出後詢問是否建立 Connection stub
/connection-query "..." --file-back thought      # 輸出後詢問是否建立 Thought candidate
/connection-query "..." --file-back none         # 只輸出，不歸檔（預設）
```

---

## Workflow（工作流程）

### Step 1: 解析問句，提取搜尋關鍵詞

```
從問句中提取：
- 核心概念詞（如 "classifier typology", "mental simulation"）
- 理論名稱（如 "Mass Noun Hypothesis", "Embodied Simulation Theory"）
- 作者/citekey 提示（如 "Huang", "Her-2012"）
- 問句類型分類：
    (a) 事實查詢（What does X say about Y?）
    (b) 比較查詢（How do X and Y differ?）
    (c) 立場查詢（What is the vault's current position on X?）
    (d) 缺口查詢（What is missing about X?）
```

### Step 2: 搜尋相關內容

**Layer A — Annotation Gears**（`ACT/0️⃣Annotation/`）
```bash
# 搜尋 Connection Gear 段落
Grep: pattern="## Connection Gear" in ACT/0️⃣Annotation/**/*.md
# 配合關鍵詞篩選
Grep: pattern="<keyword>" in ACT/0️⃣Annotation/**/*.md
```
讀取命中檔案的 Connection Gear 段落內容。不讀取全文卡片（效率控制）。

**Layer B — Connection Notes**（`ACT/1️⃣Conn/`）
```bash
Glob: ACT/1️⃣Conn/*.md
Grep: pattern="<keyword>" in ACT/1️⃣Conn/*.md
```
讀取命中 Connection notes 的相關段落。優先讀取：(1) 段落標題命中、(2) 對比表格、(3) Thought 前鏈標記（🟢/🟡/🧩）。

**Layer C — Thought Notes**（`ACT/2️⃣Thought/`）
```bash
Glob: ACT/2️⃣Thought/*.md
Grep: pattern="<keyword>" in ACT/2️⃣Thought/*.md
```
讀取命中 Thought notes 的核心主張段落。

**相關性分層**：
```
Tier 1（直接命中）：標題或段落標題含關鍵詞
Tier 2（內容命中）：正文含關鍵詞，與問句核心概念直接相關
Tier 3（間接相關）：主題相鄰，可能提供背景或對比視角
```
只有 Tier 1 + Tier 2 進入合成。Tier 3 列入「相關背景」欄位但不作為答案依據。

### Step 3: 合成有出處的答案

```
結構化整合規則：
1. 按問句類型組織答案（見 Output 格式）
2. 每個主張標注來源類型：
   - [A] = Annotation Gear 來源
   - [C] = Connection note 來源
   - [T] = Thought note 來源
3. 使用 wikilink 格式引用（如 [[🔗Linguistic theories of sortal classifiers]]、[[Her-2012/Her-2012]]）
4. 若 Tier 1/2 內容間存在矛盾 → 標記為 TENSION，不強行整合
5. 若同一主張在多層都有支持 → 標記為 CONVERGING EVIDENCE
```

**禁止行為（反幻覺規則）**：
- 禁止引用 vault 中不存在的論文或 Thought
- 禁止補充 vault 未記錄的論點（即使 AI 有外部知識）
- 禁止根據外部知識「修正」vault 中的主張
- 若 vault 內容不足以回答問題 → 誠實回報缺口，不填補

### Step 4: 識別缺口

```
缺口類型：
(a) ABSENT：問題觸及的面向在 vault 中完全沒有記錄
(b) THIN：vault 有相關線索（1-2 個 Gear）但未展開為 Connection
(c) UNRESOLVED TENSION：vault 有矛盾內容但沒有 Thought 或 Connection section 嘗試調和
(d) STALE：有相關 Connection section 但 status 很低（0-2）且無 Thought 產出
```

### Step 5: 詢問歸檔意願（若 --file-back 非 none）

根據合成答案的性質建議歸檔路徑：
```
答案屬於 "現有 Connection 的延伸" → 建議新增 section 到對應 Connection note
答案屬於 "跨多個 Connection 的整合" → 建議建立新 Connection stub
答案揭示單一可測主張 → 建議建立 Thought note candidate
缺口類型 ABSENT/THIN → 建議記錄為 Connection stub 的 Gap section
```

---

## Output（輸出）

### Query Answer Report

```markdown
# Vault Query: [問句原文]
**Generated**: YYYY-MM-DD
**Scope**: all / annotations / connections / thoughts
**Notes Searched**: N
**Relevant Hits**: N (Tier 1: X, Tier 2: Y)

---

## 📖 Vault's Current Answer

[針對問句的直接回答，整合 Tier 1+2 命中內容。
每個主張標注來源類型 [A]/[C]/[T] 並附 wikilink。]

範例：
The vault's annotations converge on the view that sortal classifiers profile inherent features of noun referents [A: [[Her-2012/Her-2012]]、[[Wu-2020/Wu-2020]]], while Connection note [[🔗Linguistic theories of sortal classifiers]] synthesizes two competing typological approaches: noun-semantics-based [C] and multiplicand-based [C]. Thought note [[🤔Noun-semantics and multiplicand taxonomies may operate at complementary analytical levels]] proposes that these may operate at different analytical levels rather than being in direct conflict [T].

---

## ⚡ Tensions Identified in Vault

[只列出 vault 內容本身存在的矛盾，不作外部評論]

| Tension | Source A | Source B | Resolution Attempt? |
|---------|----------|----------|---------------------|
| [描述矛盾] | [來源] | [來源] | [有/無，指向 Connection section 或 Thought] |

---

## 🔍 Converging Evidence

[多個層次（A+C、C+T、A+T 等）都支持同一主張的列表]

- **[主張摘要]** — Supported by [A: xxx]、[C: xxx]、[T: xxx]

---

## 🕳 Knowledge Gaps

| Gap | Type | Notes |
|-----|------|-------|
| [問題觸及的面向] | ABSENT / THIN / UNRESOLVED TENSION / STALE | [補充說明] |

---

## 📚 Sources Consulted

**Annotation Gears**:
- [[Author1-Year/Author1-Year]] — [相關 Gear 主題一句話]
- [[Author2-Year/Author2-Year]] — [相關 Gear 主題一句話]

**Connection Notes**:
- [[🔗Connection Title]] — [命中段落標題]

**Thought Notes**:
- [[🤔Thought Title]] — [核心主張一句話]

---

## 📥 File-Back Options

[只在 --file-back 非 none 時顯示]

**Option A**: Add a new section to [[🔗Existing Connection]] summarizing this query answer
**Option B**: Create a new Connection stub — suggested title: "🔗[建議標題]"
**Option C**: Create a Thought note candidate — suggested title: "🤔[建議主張句]"
**Option D**: Record gaps only — add Gap section to [[🔗Most Relevant Connection]]

Reply with A / B / C / D to proceed, or "skip" to end here.
```

---

## Quality Standards（品質標準）

### Grounding（有出處）
- [ ] 每個主張都有 [A]/[C]/[T] 標注與 wikilink
- [ ] 沒有任何主張來自 AI 外部知識（無幻覺）
- [ ] vault 不足以回答的部分誠實標記為 Gap，不填補

### Coverage（覆蓋率）
- [ ] Tier 1 命中全部讀取（無遺漏）
- [ ] Tier 2 命中按相關性取樣（不超過 15 個來源，避免過長）
- [ ] 三層（A/C/T）均有嘗試搜尋（即使某層零命中也要說明）

### Gap Identification（缺口識別）
- [ ] 每個 ABSENT 缺口有具體描述（缺少什麼）
- [ ] UNRESOLVED TENSION 要指出哪兩個來源衝突
- [ ] STALE 要說明 Connection 的 status 值

### File-Back（歸檔）
- [ ] File-back 選項與合成答案的性質相符（不強推不適合的路徑）
- [ ] 若建議新 Connection stub，標題需符合 `🔗{主題}` 格式
- [ ] 若建議 Thought candidate，標題需為原子主張句（非問題句）

---

## Integration with Other Skills（與其他 Skills 的整合）

### Upstream（上游）
- **`connection-gear-aggregate`**：此 Skill 的搜尋結果可補充 Gear Aggregation 的叢集識別
- 若 Query 揭示多個 Annotations 共享主題 → 建議接續 `/connection-gear-aggregate`

### Downstream（下游）
- **`connection-framework-synthesize`**：若 Query 發現兩個框架但尚無對比表 → 建議接續
- **`connection-tension-resolve`**：若 Query 揭示 UNRESOLVED TENSION → 建議接續
- **`thought-question-assess`**：若 File-back 選擇建立 Thought candidate → 建議接續評估可測性

### Parallel（平行）
- **`vault-report`**：Query 是問句驅動的精準查詢；Vault Report 是全域結構報告，兩者互補

---

## Examples（使用範例）

### Example 1: 事實查詢
```
User: 「vault 裡對於 C/M distinction 的操作化方式怎麼說？」

Skill: /connection-query "How is the C/M distinction operationalized in the vault?"

Output:
- Vault's Answer: Her-2012 Gear [A] + Connection section [C] 都提到三項診斷測試；Wu-2020 Gear [A] 另有集合論形式化
- Tension: DE-substitution test (Huang-2003) vs. multiplicand tests (Her-2012) — 有 Thought [T] 嘗試調和
- Gap: THIN — 操作化測試的心理語言學效度尚無 Annotation
```

### Example 2: 立場查詢 + 歸檔
```
User: 「目前 vault 對於 classifier typology 和 mental simulation 的交叉點有什麼？」

Skill: /connection-query "What does the vault say about classifier typology and mental simulation?" --file-back connection

Output:
- Vault's Answer: 兩個領域在 vault 中分屬不同 Connection notes，僅在 🤔Either theoretical approach... [T] 有間接橋接
- Gap: ABSENT — 沒有 Connection note 或 Annotation Gear 直接討論兩者的交叉
- File-Back: Option B — 建立新 Connection stub "🔗Classifier Typology and Simulation Interface"
```

### Example 3: 缺口導向查詢
```
User: 「關於 DE-insertion test 的信效度，vault 裡有什麼？」

Skill: /connection-query "What does the vault say about the validity of the DE-insertion test?" --scope connections

Output:
- Vault's Answer: [C] 🔗Linguistic theories of sortal classifiers 有 🧩 Thought 標記指向此問題
- Tension: DE-insertion 作為語法測試 [C] vs. 作為韻律邊界標記 [T: 🤔DE prosodic boundary]
- Gap: UNRESOLVED TENSION — 兩種詮釋在 vault 中並存，沒有調和嘗試
- 建議: /connection-tension-resolve "🔗Linguistic theories of sortal classifiers"
```

---

## Scope Placement Recommendation（範疇歸屬建議）

### 應歸屬 connection-workflow-manager，而非獨立 vault-level skill

理由如下：

**1. 查詢對象以 Connection notes 為核心**
此 skill 的主要知識整合點是 Connection notes。Annotation Gears 和 Thought notes 是補充來源，但 Connection notes 是理論綜合的中樞。查詢邏輯天然符合 connection-workflow-manager 的職責範圍。

**2. 查詢結果服務 Connection 發展決策**
Query 輸出的主要用途是：發現缺口 → 建議新 Connection、發現張力 → 接續 `/connection-framework-synthesize` 或 `/connection-tension-resolve`。這些後續動作都在 connection-workflow-manager 的協調範圍內。

**3. 與 vault-report 的分工**
`/vault-report` 是全域結構性報告（哪些筆記缺少連結、哪些 Annotations 尚未 Gear）。`/connection-query` 是問句驅動的精準語意查詢。兩者互補，但 `/connection-query` 的語意整合性質更靠近 connection-workflow-manager 的「框架綜合」工作。

**4. 若未來需要升級為 vault-level**
當 vault 規模擴大到需要跨越下游研究層（Questions、Projects）做查詢時，可考慮升級為獨立的 `vault-query` skill，並將 connection-query 作為其 ACT 層的專門模組。現階段不需要過度設計。

---

## Troubleshooting（疑難排解）

| 問題 | 解決方案 |
|------|----------|
| 搜尋命中過多（>15 Tier 2 來源） | 縮小範圍 (`--scope`) 或重新表述問句，提高特異性 |
| 零命中（所有層都無相關結果） | 回報 ABSENT Gap；建議用 `/connection-gear-aggregate` 確認是否有未 Gear 的相關 Annotations |
| 命中內容互相矛盾，難以合成 | 不強行整合；完整呈現 TENSION；建議接續 `/connection-tension-resolve` |
| 使用者問的是外部知識（非 vault 內容） | 明確說明此 skill 只讀 vault 內容；建議使用其他工具查詢外部文獻 |

---

## Related Documentation（相關文件）

- **Dashboard**: `ACT/ACT space.md`
- **Related Skills**: `connection-gear-aggregate`, `connection-framework-synthesize`, `connection-tension-resolve`, `vault-report`
- **Conceptual Inspiration**: Karpathy (2026-04-03) — LLM Knowledge Base Query Operation

---

## Version History

- **2026-04-06**: Initial creation — Karpathy-style Query operation for ACT vault; covers Annotation Gears, Connection notes, Thought notes; grounded answer + gap identification + optional file-back
