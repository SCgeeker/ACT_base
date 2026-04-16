---
name: thought-question-challenge
description: >
  Challenge a Thought note to surface testable questions when no obvious Question candidates exist; classifies claims and probes with bilingual questions.
  使用時機：Thought 有趣但不知道能問什麼研究問題、Thought 內容豐富但 Question 方向不明、想深化理論探索。
  觸發詞：「挑戰 Thought」「question challenge」「這個 Thought 能問什麼」「發掘問題」「探索 Thought」「surface questions」「classify claims」。
  當 Thought 豐富但 Question 方向不明確時，應使用此 skill 而非直接跳到 question-scope-sharpen。
argument-hint: <thought-note-path>
allowed-tools: Read, Glob, Grep, Edit
user-invocable: true
reusable: true
---

# Thought Question Challenge Skill

Challenge a Thought note to surface hidden testable aspects when no obvious Question candidates exist.

---

## Purpose

For Thought notes that lack clear candidate questions, this skill:

1. **Classifies claims** in the Thought note
2. **Probes with challenge questions** to surface testable aspects
3. **Updates Connection note** with emoji status markers
4. **Triggers writing improvement** for existing Question Origin sections

### When to Use This Skill vs. `/thought-question-assess`

| Situation | Skill |
|---|---|
| Thought has NO obvious question candidates | `/thought-question-challenge` (this skill) |
| Thought already HAS candidate questions listed | `/thought-question-assess` |

---

## Input

```
/thought-question-challenge "🤔Thought note title"
```

---

## Workflow

### Step 1: Read Thought Note and Context

```
1. Read target Thought note (full content)
2. Read parent Connection note (origin_source)
3. Scan linked Annotation cards referenced in the Thought
4. Identify the Thought's central thesis (title = atomic claim)
5. Check if any Question notes already link to this Thought
```

### Step 2: Classify Claims

Examine the Thought note and classify each major claim:

| Category | Definition | Marker |
|---|---|---|
| **Testable prediction** | Has operationalizable variables, competing predictions possible | 🔬 |
| **Theory fragment** | Interesting but not yet operationalizable | 🧩 |
| **Literature summary** | Describes existing findings without novel claim | 📖 |
| **Bridge claim** | Connects two frameworks but isn't independently testable | 🌉 |

**Output format:**

```markdown
## Claim Classification: 🤔[Title]

| # | Claim | Category | Rationale |
|---|---|---|---|
| 1 | [claim text or block ref] | 🔬 Testable | [why testable] |
| 2 | [claim text or block ref] | 🧩 Fragment | [what's missing] |
| 3 | [claim text or block ref] | 📖 Summary | [no novel prediction] |
| 4 | [claim text or block ref] | 🌉 Bridge | [could decompose into...] |
```

### Step 3: Challenge Questions (Dynamic Bilingual)

Generate probing questions adapted to the classification results.

**Language mode selection:**

| Stage | Language | Rationale |
|---|---|---|
| **Exploration** — no testable claims found yet | L1 (Chinese) only | Native language for fluent initial thinking |
| **Extraction** — testable claims identified | Bilingual (L1+L2) | Code-switching forces conceptual re-encoding |

**Exploration mode (L1 only):**
Present questions in Chinese to help the researcher think freely about the Thought's content:

```
這個主張的核心機制是什麼？能否拆解成更小的可測試單元？

如果這個理論片段是對的，在實驗中應該觀察到什麼現象？

哪些已有的實驗範式可以用來測試這個想法？
```

Generate 3-5 questions tailored to the specific Thought content. Questions should be **dynamic** — shaped by the specific claims, not generic templates.

**Extraction mode (bilingual):**
For claims classified as 🔬 Testable, present bilingual probing to sharpen precision:

```
What specific variable would you manipulate to test this?
你會操弄什麼具體變數來測試這個主張？

What would the competing theory predict differently?
競爭理論會預測什麼不同結果？

What's the boundary condition where this prediction might fail?
這個預測在什麼條件下可能不成立？

If you observe no effect, what does that mean for the theory?
如果你觀察不到效果，對這個理論意味著什麼？
```

Generate 3-5 bilingual question pairs tailored to each testable claim.

### Step 3.5: Source Grounding Check

Before presenting challenge questions as candidate Question titles, verify that **key terms** in each suggestion can be traced to vault sources.

**For each candidate question suggested in Step 3:**

1. Extract key conceptual terms (e.g., "attractor metaphor", "profiling strength", "core-boundary distinction")
2. Search the Thought note's source links and parent Connection for each term
3. Classify grounding status:

| Status | Definition | Action |
|---|---|---|
| **GROUNDED** | Term traces to specific Annotation card(s) | Safe to use as Question seed |
| **SYNTHESIS** | Term is researcher's own conceptual creation (in Thought title/body, not in any source card) | ⚠️ Flag: "此術語為綜合性概念，vault 中無直接來源。建議：(a) 改用可追溯的術語重構問題，或 (b) 確認這是你有意發展的新概念" |
| **AMBIGUOUS** | Term appears in sources but with different scope or meaning | ⚠️ Flag: "此術語在來源中有不同用法，需釐清哪個意涵構成 Question 基礎" |

**Output format (inserted into Challenge Report):**

```markdown
## 2.5 Source Grounding Check

| Candidate Question | Key Term | Status | Source | Note |
|---|---|---|---|---|
| What is the source of attractor metaphor? | attractor metaphor | ⚠️ SYNTHESIS | — | Thought 標題用語，無 Annotation 來源 |
| What determines core vs boundary classifiers? | core-boundary | GROUNDED | [[Her-2012a-024]], [[Gao-2009-018]] | 多源交叉驗證 |

### ⚠️ Grounding Warnings
- **"attractor metaphor"**: 此術語出現在 Thought 標題但無法追溯到任何 Annotation card。如果建立 Question，需先確認理論來源或改用可追溯的術語。
```

**Design rationale**: This check prevents the skill from generating plausible-sounding but untraceable Question candidates. The researcher should know *before* creating a Question note whether its core terms have vault provenance or require external sourcing.

### Step 4: Update Connection Note Status

Find the parent Connection note and add/update emoji marker beside the Thought link.

**Emoji legend:**

| Emoji | Meaning |
|---|---|
| ⚪ | Not yet challenged |
| 🟡 | Challenged — testable claims found, no Question yet |
| 🟢 | Has Question note(s) created |
| 🧩 | Challenged — theory fragments only, needs development |

**Update location:** In the Connection note body, add emoji before the Thought link:

```markdown
- 🟡 [[🤔Thought title]] — 2 testable claims, 1 fragment
```

**Do NOT modify** the Connection note's `thought:` frontmatter list — emoji markers go in the body text only.

### Step 5: Trigger Writing Improvement

If the Thought already has associated Question notes with content in "Question Origin" or "Working Reflections":

1. Identify the Question notes that link to this Thought
2. Read their current Question Origin content
3. Use the challenge findings (classification + probing questions) as context
4. Apply `/thought-refine` style improvements to the Question Origin narrative
5. Preserve 100% of human content — only improve expression and suggest connections

**Output:** Suggested improvements to Question Origin text, presented as recommendations (not auto-applied).

---

## Output Structure

The complete skill output has 4 sections:

```markdown
# Challenge Report: 🤔[Title]
**Generated**: YYYY-MM-DD
**Parent Connection**: [[🔗Connection title]]

## 1. Claim Classification
[Table from Step 2]

## 2. Challenge Questions
[L1 or bilingual questions from Step 3]

## 2.5 Source Grounding Check
[Grounding table + warnings from Step 3.5]

## 3. Connection Status Update
[What was updated on the Connection note, with emoji]

## 4. Question Origin Improvement (if applicable)
[Suggested improvements for existing Question notes]
```

---

## Growth Design

This skill is designed to **evolve with the vault's paper collection**:

- Challenge questions become more domain-specific as more Annotations accumulate
- Classification accuracy improves as the researcher builds theoretical context
- The skill references existing Connection frameworks and Annotation cards to ground its probing
- Over time, the challenge questions surface deeper, more specific testable aspects

---

## Quality Standards

### Classification Quality
- [ ] Every major claim in the Thought note is classified
- [ ] Categories are justified with specific rationale
- [ ] Block references (^blockid) used where available
- [ ] No claim left unclassified

### Challenge Question Quality
- [ ] Questions are dynamic — specific to THIS Thought, not generic
- [ ] L1 questions read naturally in Chinese
- [ ] Bilingual questions have genuine conceptual alignment (not literal translation)
- [ ] Questions open new angles, not repeat what the Thought already says

### Source Grounding Quality
- [ ] Every candidate question's key terms checked against vault sources
- [ ] SYNTHESIS terms flagged with explicit warning
- [ ] AMBIGUOUS terms flagged with clarification request
- [ ] No candidate question presented without grounding status

### Connection Update Quality
- [ ] Emoji marker placed in body text, not frontmatter
- [ ] Brief summary beside the marker
- [ ] Existing content not disrupted

### Human Decision Preserved
- [ ] Skill produces report and suggestions, not mandates
- [ ] Human decides which claims to pursue as Questions
- [ ] Writing improvements are recommendations, not auto-edits
- [ ] No automatic Question note creation

---

## Integration with Other Skills

### Upstream:
- **`/thought-provenance-audit`**: Run before challenge to ensure claims are well-sourced
- **`/thought-refine`**: Can improve Thought writing first for clearer challenge

### Downstream:
- **`/thought-question-assess`**: After challenge surfaces candidates, assess readiness
- **`/thought-refine`**: Triggered for Question Origin writing improvement
- **qsp-workflow-manager**: Human creates Question notes based on challenge findings

### Coexistence with `/thought-question-assess`:
```
/thought-question-challenge → surfaces WHAT is testable
                                    ↓ human creates Question
/thought-question-assess → evaluates IF it's ready to promote
                                    ↓ if PROMOTE
                           qsp-workflow-manager picks up
```

---

## Examples

### Example 1: Thought with hidden testable claims
```
User: /thought-question-challenge "🤔Cognitive saliency bridges typological linguistics and processing research as probabilistic attractor"

Output:
- Claim 1: Cognitive saliency as probabilistic attractor → 🔬 Testable
  (操弄 saliency level, 測量 classifier processing RT)
- Claim 2: Bridges typological and processing traditions → 🌉 Bridge
  (connects two frameworks, not independently testable)

Challenge Questions (bilingual for Claim 1):
  What counts as "high" vs "low" cognitive saliency for a classifier?
  什麼算是量詞的「高」vs「低」認知顯著性？
  ...

Connection update: 🟡 beside Thought link on 🔗Linguistic theories...
```

### Example 2: Thought with only theory fragments
```
User: /thought-question-challenge "🤔D-M sequences are phrasal not lexical despite historical compound terminology"

Output:
- Claim 1: Phrasal vs lexical status → 🧩 Fragment
  (structural claim, needs operationalization)
- Claim 2: Historical terminology misleads → 📖 Summary
  (describes existing finding)

Challenge Questions (L1 only):
  這個結構性主張如何轉化為可測量的行為差異？
  如果 D-M 是短語層級，在處理時間上應該和 N-CL 複合詞有什麼不同？
  ...

Connection update: 🧩 beside Thought link
```

---

## Related Documentation

- **Coexisting skill**: `/thought-question-assess` (readiness evaluation)
- **Writing skill**: `/thought-refine` (triggered for Question Origin improvement)
- **Question Spec**: `Question Iteration Spec.md`
- **Dashboard**: `ACT/ACT space.md`

---

## Version History

- **2026-02-18b**: Added Step 3.5 Source Grounding Check (QsP Iterating Phase 3 pilot feedback)
  - Verifies candidate question key terms trace to vault Annotation cards
  - Three grounding statuses: GROUNDED / SYNTHESIS / AMBIGUOUS
  - Prevents untraceable Question candidates from being created without warning
  - Triggered by "attractor metaphor" case: Thought title term had no vault source
- **2026-02-18**: Initial creation (QsP Iterating Phase 2)
  - Claim classification framework (testable/fragment/summary/bridge)
  - Dynamic bilingual challenge (L1 exploration / L1+L2 extraction)
  - Connection emoji status markers
  - Writing skill trigger for Question Origin
  - Coexists with `/thought-question-assess`
