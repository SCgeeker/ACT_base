---
name: annotation-gear-coaching
description: >
  協助撰寫 Connection Gear 的 4 階段人機協作循環，從 Card Review 到組裝完整 Gear。
  使用時機：完成 Card Review 後、準備提煉跨論文洞見、要開始撰寫 Connection Gear、建立跨論文理論連結。
  觸發詞：「寫 Gear」「Gear Coaching」「Phase 1」「提煉洞見」「啟動 Gear」「Connection Gear」「開始寫 Gear」「幫我寫 Gear」。
  只要使用者提到要寫 Gear，就應使用此 skill 的 4 階段流程，不要直接嘗試撰寫 Gear 內容。
argument-hint: <citekey> [--phase 1|2|3|4]
allowed-tools: Read, Glob, Grep, Write, Edit
---

# Connection Gear Coaching

4 階段人機協作循環，從原子卡片提煉高價值洞見並建構 Connection Gear。

## 語言策略（2026-02-07 更新）

**Connection Gear 必須使用英文**

**理由**：
- Connection Gear 是**跨論文綜合**的準備階段
- 英文作為國際學術語言，便於後續 Connection 筆記的框架整合
- 標準化語言促進不同 Annotation 的 Gears 之間的理論對話

**工作流程語言分層**：
| 階段 | 語言 | 原因 |
|------|------|------|
| Card Review | 中文 | 本地理解、術語一致性 |
| Collaborated Annotations | 中文 | 閱讀流暢性、保留語言事實 |
| **Connection Gear** | **英文** | 跨論文綜合、國際協作 |
| Connection 筆記 | 英文 | 理論框架整合、學術標準化 |

**執行要點**：
- Phase 1-4 的所有輸出必須使用英文
- 引用中文卡片標題時保持原文（Obsidian 自動處理跨語言連結）
- 中文專有名詞保留拼音標註（如「量詞 *liang4ci2*」）

## 協作循環總覽

```
Phase 1: Card Synthesis (AI 主導)
    AI 掃描卡片 → 提煉 5-7 候選洞見
    輸出：卡片摘要 + 候選洞見清單
              ↓
Phase 2: Human Selection (人類主導)
    審閱候選 → 選擇 3-5 個 → 標記研究相關性
    輸出：確認的洞見 + 研究方向
              ↓ ↺ (可迭代)
Phase 3: Deep Dialogue (協作)
    AI 提問深化 ←→ 人類回答補充
    輸出：深化描述 + 連結建議
              ↓
Phase 4: Gear Assembly (人類主導 + AI 審閱)
    人類撰寫草稿 → AI 檢查完整性
    輸出：完成的 Connection Gear
```

## Phase 1: AI 卡片綜合

**執行步驟**：
1. 掃描所有原子卡片 (`cards/Author-Year-*.md`)
2. 識別主題叢集（哪些卡片談同一概念）
3. 提煉 5-7 候選洞見（標記 ⭐ 高重要性）
4. 標註關鍵卡片（🔑）
5. 識別理論框架輪廓

**輸出格式**：參見 [phase-templates/phase1-synthesis.md](phase-templates/phase1-synthesis.md)

**品質標準**：
- 涵蓋所有主題叢集
- 洞見具體且可追溯到卡片
- 標記與現有 Connections 的潛在關聯

---

## Phase 2: 人類選擇

**引導問題**：
1. 哪些候選洞見與你的研究最相關？
2. 標記 ✅ 選擇 / ❌ 暫不選
3. AI 有沒有漏掉你認為重要的洞見？
4. 這些洞見要連到哪個 Connection？

**Multi-Gear Split（2026-03-19 新增）**：

一篇 Annotation 可以產生**多個獨立 Gear**，每個 Gear 對應不同的理論貢獻。當人類在 Phase 2 將洞見歸組到不同 Gear 時：
- 每個 Gear 應有清晰的單一主張（atomic claim）
- 在 Gear 佔位符中列出各 Gear 的標題（`<!-- Gear A: ... -->`）
- Phase 3 問題按 Gear 分組（見下方）
- `geared` frontmatter 以 boolean `true` 標記（不列 Gear 列表）

**輸出格式**：參見 [phase-templates/phase2-selection.md](phase-templates/phase2-selection.md)

---

## Phase 3: 深度對話

**AI 應主動提問**：
- 「這個洞見與你的 [[🔗xxx]] 有什麼關係？」
- 「這與 @OtherAuthor-Year 的觀點有張力嗎？」
- 「你想探索什麼待解問題？」
- 「這個發現如何改變你對 X 的理解？」

**協作模式**：
```
🤖 AI: [提問或建議]
✍️ Human: [回答或修正]
🤖 AI: [深化或確認]
   ↺ 重複 2-4 輪
```

**Multi-Gear Phase 3（2026-03-19 新增）**：

當 Phase 2 產生多個 Gear 時，Phase 3 問題**按 Gear 分組**，每個 Gear 2 個聚焦問題：
```
### Gear A — [Gear 主張]
Q-A1: [針對 Gear A 的理論連結問題]
Q-A2: [針對 Gear A 的跨論文張力問題]

### Gear B — [Gear 主張]
Q-B1: [...]
Q-B2: [...]
```
問題存入 Annotation 檔案的 `# Gear Coaching Notes` 段落，以 `✍️ **Your elaboration:**` 結尾等待人類回答。

**輸出格式**：參見 [phase-templates/phase3-dialogue.md](phase-templates/phase3-dialogue.md)

---

## Phase 4: Gear 組裝

**Gear Sentence Style（適用 AI 起草或 AI 審閱）**

Connection Gear 使用英文，並遵守以下句型規則（與 `thought-refine` / `question-refine` 一致）：

1. No em-dashes (—) for clause connection → split into separate sentences or use explicit connectives ("This produces," "Because," "Therefore")
2. No parentheses for inline lists → use "including X, Y, and Z" pattern
3. No relative clauses (which/that/who) → convert to separate sentences
4. No subordinate clauses where a direct sentence works → prefer Subject-Verb-Object pattern

**Failure example** (from 2026-03-07 session):
- ❌ "The effect is bounded within 1–4 objects — the range of subitization, where rapid enumeration operates."
- ✅ "The effect is bounded within 1–4 objects. This range corresponds to subitization. Rapid and exact enumeration is possible in this range."

**Additional Gear quality rules（2026-03-19 新增）**：

5. Self-links require judgment → When the paper's own authors appear alongside other cited authors, use `[[Author-Year|Author & Co.]]` to aid disambiguation. When the author name is the sole reference in a passage and linking adds no navigational value, use plain text.
   - ✅ "[[Jiang-2022|Jiang et al.]] frame this as... This aligns with [[Her-2010a|Her & Hsieh's (2010)]]..." (self-link disambiguates among multiple cited papers)
   - ❌ "[[Her-2020b|Her & Tsai]] ground the demolition..." (sole reference in passage, self-link is redundant)

6. No cross-language examples in English Gear → Chinese or other non-English examples in an English Gear obscure rather than illustrate the argument. Replace with English description or omit.
   - ❌ "For example, '一點兒水' versus '水一點兒' are different in syntactic and semantic levels."
   - ✅ "Free movement of N within the phrase would dissolve the structural basis for C/M's semantic relationship with N."

**人類撰寫後，AI 檢查清單**：
- [ ] 核心洞見是否涵蓋關鍵卡片？
- [ ] 理論框架是否清晰？
- [ ] 潛在連結是否明確？
- [ ] 待解問題是否具體？
- [ ] 句型符合 Gear Sentence Style（無 em-dash、無括弧清單、無關係子句、無從屬子句）？
- [ ] 無 self-link（作者名用純文字）？
- [ ] 無非英文範例（改用英文描述）？
- [ ] geared: true frontmatter 已更新？

**輸出格式**：參見 [phase-templates/phase4-assembly.md](phase-templates/phase4-assembly.md)

---

## Phase 轉換指令

| 情境 | 指令範例 |
|------|---------|
| 啟動 Phase 1 | `/annotation-gear-coaching Author-2025` |
| 指定 Phase | `/annotation-gear-coaching Author-2025 --phase 2` |
| 從 Card Review 接續 | 「我已修訂 Card Review，請啟動 Phase 1」 |
| 選擇後繼續 | 「我選了洞見 1, 2, 4，請啟動 Phase 3」 |

---

## 卡片引用模式

```markdown
// 直接引用
[[cards/Author-Year-003|情境化的概念]]

// 區塊引用（若卡片有區塊 ID）
[[cards/Author-Year-005#^core-claim]]

// 摘要引用
如卡片 003-007 所述，Barsalou 區分了...
```

---

## 完成標準

Gear 完成後：
1. 更新 frontmatter：`geared: ["🔗TargetConnection"]`
2. 通知 Connection Manager：「@Author-Year 的 Gear 已完成，可納入 [[🔗xxx]]」
3. Connection Manager 接手進行框架綜合

---

## 下一步

Gear 完成後，可使用：
- `/annotation-cross-link {citekey}` - 識別跨論文連結
- 或交由 `connection-workflow-manager` 進行框架綜合

---

## Phase 轉換邏輯（設計決定）

**採用方案**：**純對話式 + 人類啟動詞**

**設計理由**：
- Phase 之間可能迭代多次（例如從 Phase 3 退回 Phase 2 重選洞見）
- 人類使用者透過啟動詞掌控流程節奏
- 無需額外狀態追蹤，保持系統輕量

**啟動詞範例**：

| 動作 | 啟動詞 |
|------|--------|
| 前進到下一 Phase | 「進入 Phase 2」「繼續深化」「開始組裝」 |
| 退回上一 Phase | 「回到 Phase 2 重選」「重新提煉」「調整候選」 |
| 條件式前進 | 「如果洞見 1 深化完成，進入 Phase 4」 |
| 暫停 | 「先到這裡，下次繼續 Phase 3」 |

**AI 行為**：
- 每個 Phase 輸出末尾提供「下一步建議」
- 不主動追蹤狀態，依靠人類指示
- 支援任意 Phase 跳轉（非線性工作流程）

## 相關資源

- [Connection Gear Template](Templates/Connection%20Gear%20Template.md)
- [ACT space](ACT/ACT%20space.md) - ACT 儀表板
