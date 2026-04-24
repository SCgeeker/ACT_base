---
name: connection-framework-synthesize
description: >
  Synthesize multiple theoretical frameworks into coherent integration with comparison tables. 將多個競爭理論框架綜合為整合分析，生成對比表與統一框架。
  使用時機：Connection 綜合 2+ 競爭理論、需要理解框架異同、QsP 設計多框架研究、準備撰寫理論整合 Thought。
  觸發詞：「框架綜合」「理論對比」「framework synthesis」「比較框架」「整合理論」「多個理論」「理論異同」「synthesize」。
  只要涉及兩個以上理論框架的比較或整合，就應使用此 skill 而非手動比對。
argument-hint: <note-path-or-citekeys> [--output-format table|narrative]
allowed-tools: Read, Glob, Grep, Write, Edit
user-invocable: true
reusable: true
---

# Framework Synthesis Skill

將多個理論框架綜合為連貫的整合分析，適用於 Connection、Thought 和 QsP 筆記。

---

## Purpose（目的）

對多個理論框架進行系統性綜合，產生：

1. **Comparison Table**（對比表格）
   - ≥3 個對比維度（如有理論衝突）
   - 每個儲存格連結來源 (THE FIRST RULE)
   - 清晰呈現框架差異

2. **Core Disagreement Statement**（核心分歧陳述）
   - 僅在框架衝突時產生
   - 具體指出理論張力點
   - 連結對應的證據與主張

3. **Integration Narrative**（整合敘事）
   - 綜合或調和策略
   - ≥1 個可測試的預測（若涉及調和）
   - 流暢的學術段落（非列點式）

---

## Input（輸入）

### 模式 1：從 Note 路徑
```
/connection-framework-synthesize "🔗Mental Simulation Mechanisms"
```
讀取 Connection note 內容，識別需要綜合的框架

### 模式 2：指定 Citekeys
```
/connection-framework-synthesize @Smith-2020 @Jones-2021 @Chen-2022
```
直接從指定論文的 Gears 提取框架

### 模式 3：指定輸出格式
```
/connection-framework-synthesize "🔗xxx" --output-format narrative
```
- `table`: 產生 Markdown 對比表 (預設)
- `narrative`: 產生純敘事段落（適合成熟 Connections）

---

## Workflow（工作流程）

### Step 1: 框架識別
```
1. Read 目標 note 或 Annotation Gears
2. 識別理論框架：
   - Framework 名稱（如 "Embodied Simulation Theory"）
   - 主要倡導者（如 @Barsalou-2008）
   - 核心主張摘要
3. 判斷是否存在理論衝突
```

### Step 2: 對比維度設計
```
若框架衝突 → 設計 ≥3 個對比維度：
- 典型維度：
  1. Core Mechanism（核心機制）
  2. Empirical Evidence（實證證據）
  3. Scope of Application（適用範圍）
  4. Predictions（預測）
  5. Methodological Approach（方法論）

若框架互補 → 設計整合維度：
- 如：各框架在不同認知層次的貢獻
```

### Step 3: 對比表格生成
```markdown
| Dimension | Framework A [@Source1] | Framework B [@Source2] | Framework C [@Source3] |
|-----------|------------------------|------------------------|------------------------|
| **Core Mechanism** | [[Author1-2020-005.md\|Perceptual simulation]] is necessary | [[Author2-2021-010.md\|Linguistic association]] suffices | [[Author3-2022-015.md\|Hybrid]] approach |
| **Empirical Evidence** | [[Author1-2020-012.md\|Motor disruption]] impairs comprehension | [[Author2-2021-018.md\|Symbolic priming]] equally effective | [[Author3-2022-020.md\|Context-dependent]] effects |
| **Scope** | Action verbs, concrete concepts | Abstract concepts, linguistic contexts | Integrative across domains |
```

**品質檢查**：
- [ ] 每個儲存格有來源連結
- [ ] ≥3 個對比維度（衝突框架）
- [ ] 對比維度有理論意義（非任意）

### Step 4: 核心分歧陳述（若有衝突）
```markdown
**Core Disagreement**:
Framework A (Smith-2020) claims that [[Smith-2020-005.md|perceptual-motor simulation is *necessary*]] for conceptual processing, providing evidence from [[Smith-2020-012.md|motor disruption studies]]. In contrast, Framework B (Jones-2021) argues that [[Jones-2021-010.md|linguistic association]] is sufficient, citing [[Jones-2021-018.md|symbolic priming effects]] that occur without motor involvement. Framework C (Chen-2022) proposes a [[Chen-2022-015.md|hybrid account]], suggesting [[Chen-2022-020.md|context determines]] whether simulation or association dominates.
```

### Step 5: 整合敘事
```markdown
**Integration Strategy**:

採用 **Domain Partitioning** 調和策略：
- Framework A applies to [[Smith-2020-008.md|action verbs and concrete concepts]]
- Framework B applies to [[Jones-2021-020.md|abstract concepts in rich linguistic contexts]]
- Framework C provides [[Chen-2022-025.md|meta-framework for context-sensitivity]]

**Testable Prediction**:
Motor disruption should impair comprehension of [[Smith-2020-005.md|action verbs]] (e.g., "kick", "grasp") MORE than [[Jones-2021-015.md|abstract verbs]] (e.g., "think", "believe"). If so, this supports the domain-partitioning reconciliation.
```

---

## Output（輸出）

### 標準格式（Markdown）

````markdown
# Framework Synthesis: Mental Simulation Mechanisms
**Generated**: 2026-02-08
**Frameworks Analyzed**: 3
**Conflict Detected**: Yes

---

## 📊 Framework Comparison Table

| Dimension | Embodied Simulation [@Smith-2020] | Linguistic Association [@Jones-2021] | Hybrid Account [@Chen-2022] |
|-----------|-----------------------------------|--------------------------------------|------------------------------|
| **Core Mechanism** | [[Smith-2020-005.md\|Perceptual-motor simulation]] is necessary for comprehension | [[Jones-2021-010.md\|Linguistic associations]] are sufficient | [[Chen-2022-015.md\|Context-dependent integration]] of both |
| **Empirical Evidence** | [[Smith-2020-012.md\|Motor TMS disrupts]] action verb comprehension | [[Jones-2021-018.md\|Symbolic priming]] works without motor activation | [[Chen-2022-020.md\|Neural overlap varies]] by context |
| **Scope of Application** | Action verbs, concrete concepts | Abstract concepts, linguistic-rich scenarios | Cross-domain integration |
| **Key Predictions** | Motor areas causally involved | Linguistic areas alone sufficient | Context modulates mechanism |

---

## ⚡ Core Disagreement

The central tension lies in whether perceptual-motor simulation is **necessary** or merely **facilitative** for conceptual processing.

- **Necessity Claim** (Smith-2020): [[Smith-2020-005.md|Simulation is a constitutive mechanism]]. Evidence from [[Smith-2020-012.md|motor disruption studies]] shows impaired comprehension when motor areas are inhibited.

- **Sufficiency Claim** (Jones-2021): [[Jones-2021-010.md|Linguistic association alone is sufficient]]. Evidence from [[Jones-2021-018.md|symbolic priming]] demonstrates comprehension without motor activation.

- **Hybrid Position** (Chen-2022): [[Chen-2022-015.md|Both mechanisms contribute]], with [[Chen-2022-020.md|context determining reliance]]. Neural overlap between action and language varies by task demands.

---

## 🔗 Integration Narrative

The apparent conflict can be reconciled through **domain partitioning** and **context-sensitivity**.

Smith's Embodied Simulation Theory applies most strongly to [[Smith-2020-008.md|action verbs and concrete concepts]], where perceptual-motor grounding is robust. Jones' Linguistic Association Model better accounts for [[Jones-2021-020.md|abstract concepts embedded in rich linguistic contexts]], where symbolic relationships dominate. Chen's Hybrid Account provides a [[Chen-2022-025.md|meta-framework that incorporates both]], suggesting that the degree of simulation involvement depends on concept concreteness and contextual support.

This reconciliation yields a **testable prediction**: Motor disruption should disproportionately impair comprehension of action verbs (e.g., "kick", "grasp") compared to abstract verbs (e.g., "think", "believe"). Experimental dissociation of this effect would validate the domain-partitioning strategy.

---

## 🎯 Next Steps

1. **Expand Connection Gear**: Integrate this synthesis into [[🔗Mental Simulation Mechanisms]]
2. **Consider Thought Extraction**: The "domain partitioning" insight may warrant a separate [[🤔Thought note]]
3. **Potential Question**: Design experiment to test the motor-disruption prediction
4. **Optional Tension Resolution**: If deeper reconciliation needed, use `/connection-tension-resolve`

---

## 📝 Metadata

**Frameworks Synthesized**:
- Embodied Simulation Theory (@Smith-2020)
- Linguistic Association Model (@Jones-2021)
- Hybrid Context-Dependent Account (@Chen-2022)

**Synthesis Type**: Reconciliation via domain partitioning
**Output Format**: Table + Narrative
**Conflict Severity**: Medium (reconcilable through domain specification)
````

---

## Quality Standards（品質標準）

### Comparison Table
- [ ] ≥3 dimensions if frameworks conflict
- [ ] Every cell has source link (THE FIRST RULE)
- [ ] Dimensions have theoretical significance
- [ ] Clear differences between frameworks

### Core Disagreement (if conflict)
- [ ] Specific theoretical tension identified
- [ ] Evidence from sources cited
- [ ] Disagreement is non-trivial and substantive

### Integration Narrative
- [ ] Coherent synthesis or reconciliation strategy
- [ ] ≥1 testable prediction (if reconciliation)
- [ ] Flowing academic prose (no bullet points)
- [ ] Maintains source linking throughout

---

## Reusability（可重用性）

此 Skill 可用於：

### 1. Connection Notes (ACT/1️⃣Conn/)
- 綜合多個 Annotation Gears
- 建立理論對比表
- 準備 Thought extraction

### 2. Thought Notes (ACT/2️⃣Thought/)
- 比較理論視角
- 深化理論理解
- 識別可測試的張力

### 3. Further Research
- 設計多框架研究
- 建構實驗假設
- 規劃理論檢驗

---

## Integration with Other Skills（與其他 Skills 的整合）

### Upstream（上游）
- **`connection-gear-aggregate`**: 識別需要框架綜合的 Gear 叢集
- 當 Gear Aggregation 發現理論張力時，自動建議此 Skill

### Downstream（下游）
- **`connection-tension-resolve`**: 若綜合後仍有未解張力，交接調和任務
- **`thought-refine`**: 精煉整合敘事的寫作品質

### Parallel（平行）
- **`annotation-cross-link`**: 框架綜合可揭示跨論文連結
- **P-CSO Skills**: 整合敘事可使用 `pinker-coherence` 優化流暢度

---

## Examples（使用範例）

### Example 1: Connection 框架綜合
```
User: 我的 🔗Mental Simulation Mechanisms 有三個理論框架互相衝突，請幫我做框架綜合。

Skill: /connection-framework-synthesize "🔗Mental Simulation Mechanisms"

Output:
- Comparison table (3 frameworks, 4 dimensions)
- Core disagreement: Necessity vs. Facilitation
- Integration: Domain partitioning strategy
- Testable prediction: Motor disruption differential effect
```

### Example 2: 從 Citekeys 直接綜合
```
User: 請比較 @Barsalou-2008 @Mahon-2015 @Dove-2016 的理論框架。

Skill: /connection-framework-synthesize @Barsalou-2008 @Mahon-2015 @Dove-2016

Output:
- 3-way framework comparison
- Grounded vs. Hybrid vs. Linguistic accounts
- Reconciliation via multi-level processing
```

### Example 3: 純敘事輸出
```
User: 我不需要表格，直接給我敘事整合就好。

Skill: /connection-framework-synthesize "🔗xxx" --output-format narrative

Output:
- No comparison table
- Direct integration narrative
- Maintains source linking
```

---

## Troubleshooting（疑難排解）

### 問題 1：框架定義模糊
**症狀**：無法清楚區分不同框架

**解決方案**：
1. 回到 Annotation Gears 確認框架名稱
2. 使用主要倡導者區分（如 "Barsalou's Grounded Cognition"）
3. 若框架過於相似，考慮合併為單一視角

### 問題 2：對比維度選擇困難
**症狀**：不確定用哪些維度對比

**解決方案**：
1. 預設維度：Core Mechanism, Evidence, Scope, Predictions
2. 參考論文中的對比（作者如何區分理論）
3. 選擇能揭示理論張力的維度

### 問題 3：整合敘事缺乏可測試預測
**症狀**：調和策略過於模糊

**解決方案**：
1. 回到理論差異，尋找可實驗操縱的變項
2. 參考論文中的實驗設計
3. 若無法產生預測，標記為「描述性整合」（非調和）

---

## Related Documentation（相關文件）

- **Template**: `Templates/Connection Gear Template.md`
- **Dashboard**: `ACT/ACT space.md`
- **Related Skills**: `connection-gear-aggregate`, `connection-tension-resolve`

---

## Version History（版本歷史）

- **2026-02-08**: Initial creation (Skills Migration v2.0)
- 可重用於 Connection、Thought、QsP 筆記
- 整合 THE FIRST RULE（所有主張必須連結來源）
