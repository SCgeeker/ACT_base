---
name: connection-tension-resolve
description: >
  Identify theoretical tensions and propose reconciliation strategies with testable predictions.
  識別理論框架間的衝突並提出調和策略與可測試預測，推動理論發展到實驗設計。
  使用時機：Connection 有衝突框架、Thought 探索理論矛盾、下游研究問題需要實驗分離、需要設計關鍵區別實驗。
  觸發詞：「理論衝突」「調和策略」「tension resolve」「解決張力」「reconciliation」「框架矛盾」「衝突理論」「如何調和」「衝突框架」。
  只要使用者提到兩個理論之間的矛盾或需要調和不同框架，就應使用此 skill。
argument-hint: <note-path> [--strategy domain-partitioning|multi-level|competing-mechanisms]
allowed-tools: Read, Glob, Grep, Write, Edit
user-invocable: true
reusable: true
---

# Tension Resolution Skill

識別理論張力並提出調和策略，附帶可測試的預測。

---

## Purpose（目的）

當理論框架之間存在實質衝突時，此 Skill 提供：

1. **Tension Identification**（張力識別）
   - 精確定位理論分歧點
   - 區分「表面矛盾」vs.「深層衝突」
   - 判斷張力是否可調和

2. **Reconciliation Strategies**（調和策略）
   - Domain Partitioning（領域分割）
   - Multi-Level Processing（多層次處理）
   - Competing Mechanisms（競爭機制）
   - Integration via Constraints（限制條件整合）

3. **Testable Predictions**（可測試預測）
   - 實驗設計建議
   - 關鍵操縱變項
   - 預期結果模式
   - 理論檢驗標準

4. **Research Trajectory**（研究軌跡）
   - 連結到潛在 Thought notes
   - 建議 Question formulation
   - 指向 Project design

---

## Input（輸入）

### 基本模式
```
/connection-tension-resolve "🔗Mental Simulation Mechanisms"
```
讀取 Connection note，自動識別張力並建議策略

### 指定調和策略
```
/connection-tension-resolve "🔗xxx" --strategy domain-partitioning
```
強制使用特定策略：
- `domain-partitioning`: 不同領域適用不同理論
- `multi-level`: 不同認知層次使用不同機制
- `competing-mechanisms`: 設計實驗分離機制

---

## Reconciliation Strategies（調和策略庫）

### Strategy 1: Domain Partitioning（領域分割）

**適用**：理論適用於不同概念類別、刺激材料、或任務需求

**邏輯**：
```
Theory A → applies to Domain X (e.g., action verbs, concrete concepts)
Theory B → applies to Domain Y (e.g., abstract concepts, linguistic contexts)
```

**核心範例**：
```markdown
**Tension**: Embodied Simulation vs. Linguistic Association
**Resolution**: Domain Partitioning
- Embodied Simulation → action verbs, concrete concepts (sensorimotor grounding)
- Linguistic Association → abstract concepts in rich contexts (symbolic relationships)
**Testable Prediction**: Motor disruption (TMS) impairs action > abstract verb comprehension
```

---

### Strategy 2: Multi-Level Processing（多層次處理）

**適用**：理論描述不同認知層次、時間動態差異（早期 vs. 晚期處理）

**邏輯**：
```
Theory A → Level 1 (e.g., early automatic processing, < 300ms)
Theory B → Level 2 (e.g., late controlled processing, > 500ms)
Both contribute sequentially or in parallel
```

**核心範例**：
```markdown
**Tension**: Automatic Embodiment vs. Strategic Simulation
**Resolution**: Multi-Level Processing
- Early Stage (< 300ms): Automatic motor resonance (mandatory, pre-semantic)
- Late Stage (> 500ms): Strategic simulation (task-dependent, context-modulated)
**Testable Prediction**: ERP early motor activation for all verbs; late effects only under imagery task
```

---

### Strategy 3: Competing Mechanisms（競爭機制）

**適用**：理論根本不可調和，需要實驗證據分離不同機制

**邏輯**：
```
Theory A and Theory B make DIFFERENT predictions
→ Design critical experiment to dissociate mechanisms
→ Winner determined by empirical evidence
```

**核心範例**：
```markdown
**Tension**: Simulation Necessity vs. Linguistic Sufficiency
**Resolution**: Experimental Dissociation
- IV: Motor cortex TMS vs. Sham
- DV: Action verb comprehension accuracy
- Prediction A (Necessity): Accuracy drops significantly
- Prediction B (Sufficiency): Accuracy unaffected
**Status**: Unresolved, context-dependency suspected
```

---

### Strategy 4: Integration via Constraints（限制條件整合）

**適用**：理論各自正確但有適用條件，邊界條件（boundary conditions）未明確

**邏輯**：
```
Theory A holds when Constraint X is met
Theory B holds when Constraint Y is met
→ Identify constraints as the real research priority
```

**核心範例**：
```markdown
**Tension**: Strong Embodiment vs. Weak Embodiment
**Resolution**: Integration via Constraints
- Constraint Factors: Concept Concreteness, Linguistic Context, Individual Differences
- Integrated Model: Embodiment strength = f(concreteness, context, expertise)
**Testable Prediction**: 3-way interaction in fMRI
  (concrete × minimal context × motor experts → strongest motor activation)
```

> **📄 完整策略輸出範例（含所有格式細節）**：見 `references/output-example.md`

---

## Workflow（工作流程）

### Step 1: Tension Identification
```
1. Read target note (Connection, Thought, or specified Annotations)
2. Identify conflicting frameworks:
   - Theory A claims X
   - Theory B claims NOT-X (or conflicting evidence)
3. Classify tension type:
   - Surface Contradiction (terminological difference only)
   - Deep Conflict (substantive theoretical difference)
   - Pseudo-Conflict (theories operate at different levels/domains)
```

### Step 2: Strategy Selection
```
Decision Tree:
- Different domains/concepts? → Domain Partitioning
- Different processing stages? → Multi-Level Processing
- Fundamentally incompatible? → Competing Mechanisms
- Boundary conditions unclear? → Integration via Constraints
- Multiple strategies viable? → Present all options
```

### Step 3: Reconciliation Proposal
```
For chosen strategy:
1. Specify reconciliation logic
2. Map theories to domains/levels/conditions
3. Cite supporting evidence from source cards
4. Identify gaps in current knowledge
```

### Step 4: Generate Testable Predictions
```
Design critical test:
1. Independent variable (what to manipulate)
2. Dependent variable (what to measure)
3. Predicted outcome patterns for each theory
4. How results adjudicate between theories
```

### Step 5: Research Trajectory
```
Suggest next steps:
- Create Thought note for reconciliation insight?
- Formulate Question for experimental test?
- Link to existing Projects?
```

---

## Output（輸出）

輸出包含 5 個主要區塊：

1. **Header** — 日期、來源筆記、張力類型、調和策略
2. **⚡ Identified Tension** — 衝突框架各自的主張與支持證據（含 card 連結）
3. **🔧 Reconciliation Strategy** — 調和邏輯、理論分配、支持證據
4. **🧪 Testable Predictions** — 實驗設計（IV、DV、預期結果、理論判準）
5. **🎯 Research Trajectory** — 建議 Thought/Question/Project notes 名稱

**📄 完整輸出範例與格式細節**：見 `references/output-example.md`

---

## Quality Standards（品質標準）

### Tension Identification
- [ ] Precise statement of conflicting claims
- [ ] Evidence cited for both sides
- [ ] Clear why this is a substantive (not superficial) conflict

### Reconciliation Strategy
- [ ] Explicit reconciliation logic
- [ ] Domain/level/condition specifications
- [ ] Supporting evidence from sources
- [ ] Acknowledges unresolved issues

### Testable Predictions
- [ ] ≥1 concrete experimental design
- [ ] Clear IVs, DVs, predicted outcomes
- [ ] Explains how results adjudicate theories
- [ ] Feasible with current methods

### Research Trajectory
- [ ] Suggests specific Thought/Question notes
- [ ] Links to broader research program
- [ ] Identifies knowledge gaps

---

## Integration with Other Skills（與其他 Skills 的整合）

### Upstream（上游）
- **`connection-framework-synthesize`**: 框架綜合後若仍有張力，交接此 Skill
- **`connection-gear-aggregate`**: Gear 聚合識別張力，可直接調用此 Skill

### Downstream（下游）
- **`thought-question-assess`**: 調和策略可能萌發 Thought/Question
- **`thought-refine`**: 精煉調和敘事的寫作品質

### Parallel（平行）
- **P-CSO Skills**: 調和敘事可使用 `pinker-coherence` 優化論述流暢度

---

## Troubleshooting（疑難排解）

| 問題 | 解決方案 |
|------|----------|
| 張力不明顯（框架差異模糊） | 回到 `connection-framework-synthesize` 生成對比表；尋找具體預測差異（而非描述差異）；若無實質張力，標記為「互補框架」 |
| 無法產生可測試預測 | 檢查理論是否足夠具體（operational definitions）；參考原論文實驗範式；降低預測精度（定性→定量） |
| 多個策略皆適用 | 提供多種策略選項並說明各自優缺點；建議設計實驗檢驗哪個策略更佳 |

---

## Related Documentation（相關文件）

- **Dashboard**: `ACT/ACT space.md`
- **Related Skills**: `connection-framework-synthesize`, `thought-question-assess`
- **Output Example**: `references/output-example.md`
- **Scientific Foundations**: Lakatos (1970) 的理論調和策略

---

## Version History

- **2026-02-08**: Initial creation (Skills Migration v2.0) — 4 種調和策略庫
- **2026-03-07**: Refactored — extracted 155-line output example to `references/`, condensed strategy examples, updated description
