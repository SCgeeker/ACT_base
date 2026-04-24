---
name: connection-gear-aggregate
description: >
  Aggregate Connection Gears from multiple annotations to identify synthesis opportunities. 聚合多篇論文的 Annotation Gears，識別跨文獻主題與 Connection 發展機會。
  使用時機：完成 3+ Annotation Gears、準備創建新 Connection、識別哪些論文應在同一 Connection 中綜合、擴展現有 Connections。
  觸發詞：「聚合 Gears」「識別 Connection 主題」「gear aggregation」「哪些 Gears 可以連結」「建立 Connection」「跨論文綜合」「哪些論文一起」。
  完成多篇 Gear 後，應主動建議使用此 skill 規劃 Connection 方向。
argument-hint: [--citekeys <list>] [--connection-hint <existing-connection>]
allowed-tools: Read, Glob, Grep, Bash
user-invocable: true
reusable: true
---

# Gear Aggregation Skill

從多個 Annotation Gears 識別主題叢集與 Connection 發展機會。

---

## Purpose（目的）

分析多個已完成的 Annotation Gears 以：

1. **識別主題叢集**（Thematic Clusters）
   - 哪些 Gears 共享核心概念
   - 理論框架的交集與差異
   - 方法論上的共通性

2. **繪製理論張力地圖**（Theoretical Tension Map）
   - 框架之間的衝突點
   - 概念定義的歧義
   - 可測試的理論分歧

3. **建議 Connection 策略**（Connection Strategies）
   - 擴展現有 Connection vs. 創建新 Connection
   - 優先順序排序（研究影響力）
   - 跨論文綜合的最佳切入點

4. **優先順序排序**（Prioritization）
   - 理論重要性
   - 可操作性（testability）
   - 與現有研究方向的相關性

---

## Input（輸入）

### 基本模式
```
/connection-gear-aggregate
```
掃描所有已完成 Gear 的 Annotations

### 指定 Citekeys
```
/connection-gear-aggregate --citekeys @Smith-2020 @Jones-2021 @Chen-2022
```
僅分析指定論文的 Gears

### 擴展現有 Connection
```
/connection-gear-aggregate --connection-hint "🔗Mental Simulation Mechanisms"
```
分析哪些新 Gears 可納入此 Connection

---

## Workflow（工作流程）

### Step 1: 掃描 Gears
```
1. Glob: ACT/0️⃣Annotation/*/Author-Year.md
2. Read: frontmatter 檢查 geared: ["🔗xxx"]
3. Read: Connection Gear 區段內容
4. 提取核心概念、理論框架、待解問題
```

**CLI 輔助 — 反向連結映射**：

對每個已存在的 Connection note，使用 CLI 查詢哪些 Annotations 實際連結到它：
```bash
# 自動映射 Annotation → Connection 的連結關係
obsidian vault=ACT_Base backlinks path="ACT/1️⃣Conn/🔗{Connection Name}.md" counts
```

此步驟比逐一讀取每個 Annotation 的 `geared:` frontmatter 更高效：
- 一次命令即可取得完整的反向連結清單
- 包含 Obsidian 解析的所有連結類型（wikilinks、embeds、aliases）
- 可快速比對 `geared:` 標記是否與實際連結一致

### Step 2: 主題叢集分析
```
識別：
- 共同概念（如 "mental simulation", "embodied cognition"）
- 理論家族（如 Grounded Cognition 派別）
- 方法論共性（如 fMRI 研究、行為實驗）

輸出：
- Cluster 1: [概念名稱]
  - 涵蓋 Gears: @Author1, @Author2, @Author3
  - 核心主張: [摘要]
  - 關鍵差異: [對比]
```

### Step 3: 理論張力識別
```
對比框架：
- Framework A (@Author1): [主張]
- Framework B (@Author2): [反向主張]
- Tension: [衝突點]
- Testable Prediction: [可實驗檢驗的差異]
```

### Step 4: Connection 策略建議

**CLI 輔助 — Connection 成熟度評估**：

查詢每個候選 Connection 的連結密度，作為成熟度指標：
```bash
obsidian vault=ACT_Base links path="ACT/1️⃣Conn/🔗{Connection Name}.md" total
```
- 高連結密度 → 成熟 Connection，適合「張力解決」或「框架綜合」
- 低連結密度 → 年輕 Connection，適合「擴展 Gear 聚合」

```
情境 1：已有 Connection 🔗Mental Simulation
建議：擴展 Gear 聚合（+3 新論文）

情境 2：新主題浮現 "Language-Action Coupling"
建議：創建新 Connection（6 篇相關論文）

情境 3：張力過大 "Embodied vs. Symbolic"
建議：創建對比型 Connection（需框架綜合）
```

---

## Output（輸出）

### Gear Aggregation Report

```markdown
# Gear Aggregation Report
**Generated**: 2026-02-08
**Scanned Annotations**: 15
**Identified Gears**: 12

---

## 🎯 Thematic Clusters

### Cluster 1: Mental Simulation Mechanisms
**Core Concept**: Perceptual-motor simulation in conceptual processing

**Gears Involved**:
- [[Smith-2020]]: Sensorimotor grounding in verb comprehension
- [[Jones-2021]]: Simulation vs. association debate
- [[Chen-2022]]: Neural overlap between action and language

**Synthesis Opportunity**:
Create or expand **🔗Mental Simulation Mechanisms** to integrate these three frameworks.

**Key Insight**:
All three Gears discuss simulation but disagree on whether it's *necessary* (Smith, Jones) or *facilitative* (Chen).

**Recommended Action**:
Create framework comparison table (use `/connection-framework-synthesize`)

---

### Cluster 2: Embodied Number Cognition
**Core Concept**: Spatial grounding of numerical representation

**Gears Involved**:
- [[Wang-2019]]: SNARC effect meta-analysis
- [[Lee-2020]]: Finger counting and arithmetic
- [[Martinez-2021]]: Embodied math education

**Synthesis Opportunity**:
New Connection needed: **🔗Embodied Foundations of Number Cognition**

**Key Insight**:
Converging evidence from behavioral (Wang), developmental (Lee), educational (Martinez) domains.

**Recommended Action**:
Create new Connection note with multi-level synthesis

---

## ⚡ Theoretical Tensions

### Tension 1: Simulation Necessity vs. Facilitation
**Framework A**: Embodied Simulation Theory (Smith-2020, Jones-2021)
- Claim: Perceptual-motor simulation is *necessary* for comprehension
- Evidence: Disrupting motor areas impairs verb understanding

**Framework B**: Embodied Facilitation Theory (Chen-2022)
- Claim: Simulation *facilitates* but is not necessary
- Evidence: Comprehension survives motor disruption under some conditions

**Reconciliation Strategy**:
Domain partitioning (see `/connection-tension-resolve`)
- Necessary: Action verbs, concrete concepts
- Facilitative: Abstract concepts, linguistic context-rich scenarios

**Testable Prediction**:
Motor disruption should impair action-verb comprehension MORE than abstract-verb comprehension.

---

## 📊 Connection Development Strategies

### Priority 1: Expand 🔗Mental Simulation Mechanisms (HIGH)
**Action**: Aggregate 3 new Gears into existing Connection
**Timeline**: This week
**Impact**: Strengthens core theoretical framework for ongoing Projects

### Priority 2: Create 🔗Embodied Number Cognition (MEDIUM)
**Action**: New Connection from 3 clustered Gears
**Timeline**: Next 2 weeks
**Impact**: Opens new research trajectory in math cognition

### Priority 3: Resolve Simulation Necessity Tension (LOW)
**Action**: Use `/connection-tension-resolve` for reconciliation
**Timeline**: After Priority 1-2
**Impact**: Theoretical clarity for future Questions

---

## 🔗 Suggested Next Steps

1. **Immediate**: Review Priority 1 - decide if 🔗Mental Simulation Mechanisms should expand
2. **This Week**: If yes, use `/connection-framework-synthesize` for framework comparison
3. **Next Week**: Create 🔗Embodied Number Cognition from Cluster 2
4. **Optional**: Run `/connection-tension-resolve` on Simulation Necessity debate

---

## 📝 Notes

- 3 Gears not yet assigned to clusters (exploratory papers, may need future review)
- 2 Connections already exist: 🔗Mental Simulation Mechanisms, 🔗Language Grounding
- Consider cross-linking between Clusters 1 & 2 (shared embodiment theme)
```

---

## Quality Standards（品質標準）

### Cluster Identification
- [ ] 涵蓋所有完成 Gear 的 Annotations（無遺漏）
- [ ] 每個 Cluster ≥2 個 Gears（避免單論文 Connection）
- [ ] Cluster 主題明確且可區分（非模糊重疊）

### Tension Mapping
- [ ] 理論張力具體且可驗證（非泛泛而談）
- [ ] 提供可測試的預測（testable predictions）
- [ ] 引用具體 Gear 內容（有來源追溯性）

### Strategy Recommendation
- [ ] 優先順序有明確理由（研究影響、可操作性）
- [ ] 區分「擴展現有」vs.「創建新 Connection」
- [ ] 提供具體下一步行動（可執行）

---

## Integration with Other Skills（與其他 Skills 的整合）

### Upstream（上游）
- **`annotation-gear-coaching`**: 此 Skill 接收 Gear Coaching 完成的 Annotations
- 確保 Gear 已寫入 frontmatter `geared: ["🔗xxx"]`

### Downstream（下游）
- **`connection-framework-synthesize`**: 當識別到理論張力時，交接框架綜合任務
- **`connection-tension-resolve`**: 當需要調和策略時，交接張力解決任務

### Parallel（平行）
- **`annotation-cross-link`**: Gear Aggregation 可發現跨論文連結機會

---

## Examples（使用範例）

### Example 1: 初次掃描
```
User: 我完成了 5 篇論文的 Gears，請幫我聚合看看有什麼主題。

Skill: /connection-gear-aggregate

Output:
- Cluster 1: Mental Simulation (3 papers)
- Cluster 2: Spatial Cognition (2 papers)
- Recommendation: Create new 🔗Mental Simulation Mechanisms
```

### Example 2: 擴展現有 Connection
```
User: 我想擴展 🔗Mental Simulation Mechanisms，最近又完成了 3 篇新論文的 Gears。

Skill: /connection-gear-aggregate --connection-hint "🔗Mental Simulation Mechanisms"

Output:
- 3 new Gears compatible with existing Connection
- Identified 1 theoretical tension (Necessity vs. Facilitation)
- Recommendation: Use `/connection-framework-synthesize` before aggregating
```

### Example 3: 指定範圍分析
```
User: 只分析這三篇的 Gears：@Smith-2020 @Jones-2021 @Chen-2022

Skill: /connection-gear-aggregate --citekeys @Smith-2020 @Jones-2021 @Chen-2022

Output:
- All 3 Gears share "simulation" theme
- Theoretical tension identified
- Recommendation: Create comparison table with framework synthesis
```

---

## Troubleshooting（疑難排解）

### 問題 1：Gears 未標記 Connection
**症狀**：某些 Annotation 有 Gear 內容但 frontmatter 無 `geared: []`

**解決方案**：
1. 提醒使用者手動更新 frontmatter
2. 或使用 `annotation-monitor` 掃描未完成 Gears

### 問題 2：主題叢集過於分散
**症狀**：10 個 Gears 產生 10 個單論文 Clusters

**解決方案**：
1. 放寬主題定義（從具體概念到理論家族）
2. 建議使用者先累積更多 Gears
3. 提供「潛在連結」清單供未來參考

### 問題 3：無法決定擴展 vs. 新建
**症狀**：新 Gear 與現有 Connection 部分重疊

**解決方案**：
1. 提供兩種選項（擴展 A + 新建 B）
2. 標記重疊程度（30% overlap → 建議新建）
3. 讓使用者選擇策略

---

## Related Documentation（相關文件）

- **Template**: `Templates/Template, Connection Note.md`
- **Dashboard**: `ACT/ACT space.md`
- **Downstream Skills**: `connection-framework-synthesize`, `connection-tension-resolve`

---

## Version History（版本歷史）

- **2026-02-08**: Initial creation (Skills Migration v2.0)
- 基於 annotation-workflow-manager 成功遷移經驗
- 採用 Thin Orchestrator + Specialized Skills 架構