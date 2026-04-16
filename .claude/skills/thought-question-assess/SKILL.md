---
name: thought-question-assess
description: >
  Evaluate whether a Thought note is ready for Question promotion, assessing testability, theoretical depth, provenance, and prediction specificity.
  使用時機：Thought 已有足夠深度、想知道是否可以升格為 Question、準備提交 qsp-workflow-manager 前的評估。
  觸發詞：「能升格嗎」「Question assess」「Thought 成熟了嗎」「升格為 Question」「評估 Thought」「升格評估」「assess thought」「ready for question」。
  在考慮建立新 Question 之前，應先使用此 skill 評估對應的 Thought 是否就緒。
argument-hint: <thought-note-path> [--target-question-type phenomenon|mechanism|boundary|exploratory]
allowed-tools: Read, Glob, Grep
user-invocable: true
reusable: true
---

# Thought Question Assessment Skill

Evaluate Thought readiness for Question promotion and produce handoff package for qsp-workflow-manager.

---

## Purpose

Assess whether a Thought note has matured enough to become a formal research Question:

1. **Readiness Assessment** (4 criteria)
   - Testability: Can variables be operationalized?
   - Theoretical depth: Is the argument fully developed?
   - Provenance completeness: Are all claims traced?
   - Prediction specificity: Does it generate distinguishable predictions?

2. **Readiness Report**
   - Score on each criterion (Ready / Developing / Not Ready)
   - Specific gaps to address if not ready
   - Suggested next steps

3. **Handoff Package** (when ready)
   - Suggested Question formulation
   - Question type recommendation (phenomenon / mechanism / boundary / exploratory)
   - Research design hints
   - Package for qsp-workflow-manager

---

## Input

### Standard Assessment
```
/thought-question-assess "🤔general classifiers might evoke attention to mental entity"
```
Full readiness assessment with all 4 criteria.

### Targeted Assessment
```
/thought-question-assess "🤔xxx" --target-question-type mechanism
```
Assess with specific Question type in mind, adjusting criteria weights.

---

## Readiness Criteria

### Criterion 1: Testability
```
Can the Thought's central claim be tested empirically?

Indicators of READY:
- Clear independent variable (what to manipulate)
- Clear dependent variable (what to measure)
- Existing paradigm or feasible new design
- At least one competing prediction

Indicators of NOT READY:
- Purely descriptive insight (no prediction)
- Variables too abstract to operationalize
- No known paradigm for testing
- Circular reasoning (conclusion assumed in premise)
```

### Criterion 2: Theoretical Depth
```
Is the argument fully developed?

Indicators of READY:
- Primary Reflection articulates ONE clear atomic thesis
- Thesis developed with multi-paragraph evidence synthesis
- Arguments build coherently toward a single claim
- Theoretical context established (what's known, what's unknown)

Indicators of NOT READY:
- Single undeveloped assertion
- Arguments don't connect to each other
- Missing theoretical context
- Key terms undefined
```

### Criterion 3: Provenance Completeness
```
Are all claims traced to sources?

Indicators of READY:
- /thought-provenance-audit shows 80%+ coverage
- THE FIRST RULE: 3-7+ source links
- No orphaned claims (untraced assertions)
- Key claims have paragraph-level references

Indicators of NOT READY:
- Provenance audit not yet run
- Coverage below 60%
- Multiple orphaned claims
- Below minimum source links
```

### Criterion 4: Prediction Specificity
```
Does the Thought generate specific, distinguishable predictions?

Indicators of READY:
- At least 1 specific prediction stated
- Predictions distinguish between competing theories
- Predictions are falsifiable
- Effect direction specified (not just "there will be an effect")

Indicators of NOT READY:
- No predictions beyond general expectation
- Predictions don't distinguish theories
- Unfalsifiable claims
- Only vague directional expectations
```

---

## Workflow

### Step 1: Read Thought Note and Context
```
1. Read target Thought note
2. Read parent Connection note(s)
3. Check if provenance audit exists
4. Check existing Question links (question: property)
5. Identify the Thought's central thesis (note title = atomic claim)
```

### Step 2: Assess Each Criterion
```
For each of the 4 criteria:
1. Evaluate against indicators
2. Rate: Ready / Developing / Not Ready
3. Provide specific evidence for rating
4. If not ready: identify what's missing
```

### Step 3: Calculate Overall Readiness
```
Scoring:
- Ready on all 4 criteria → PROMOTE (proceed to handoff)
- Ready on 3, Developing on 1 → ALMOST READY (specific guidance)
- Ready on 2 or fewer → NEEDS DEVELOPMENT (development plan)
- Not Ready on any → NOT READY (fundamental gaps)
```

### Step 4: Generate Report
```markdown
## Question Readiness Assessment: 🤔[Title]
**Generated**: YYYY-MM-DD
**Overall**: [PROMOTE | ALMOST READY | NEEDS DEVELOPMENT | NOT READY]

### Criterion Scores

| Criterion | Score | Key Evidence |
|---|---|---|
| Testability | Ready / Developing / Not Ready | [specific evidence] |
| Theoretical Depth | Ready / Developing / Not Ready | [specific evidence] |
| Provenance Completeness | Ready / Developing / Not Ready | [specific evidence] |
| Prediction Specificity | Ready / Developing / Not Ready | [specific evidence] |

### Gaps to Address (if not PROMOTE)
1. [Specific gap with suggestion]
2. [Specific gap with suggestion]

### Suggested Development Path
[Steps to reach readiness]
```

### Step 5: Handoff Package (if PROMOTE)
```markdown
## Handoff Package for qsp-workflow-manager

### Suggested Question Formulation
**Title**: 🕵️[Suggested Question title]
**Working Hypothesis**: [1-2 sentences]

### Question Type Recommendation
**Recommended**: [phenomenon | mechanism | boundary | exploratory]
**Rationale**: [Why this type fits]

### Research Design Hints
- **IV**: [Suggested independent variable]
- **DV**: [Suggested dependent variable]
- **Paradigm**: [Suggested experimental paradigm]
- **Key Contrast**: [What predictions distinguish theories]

### Source Thought
- **Note**: [[🤔Thought title]]
- **Parent Connection(s)**: [[🔗Connection title(s)]]
- **Provenance Score**: X/Y claims traced

### Frontmatter for New Question (must match template exactly)
```yaml
title: 🕵️[Question title]
tags:
  - state/Q
created: YYYY-MM-DD
updated: YYYY-MM-DD
origin_source: "[[🤔Thought title]]"
state: forming
project:
  -
```

> **Additional metadata** (inline fields in Memo section, NOT frontmatter):
> ```
> question_type:: phenomenon | mechanism | boundary | exploratory
> priority:: primary | secondary | exploratory
> provenance_score:: X/Y claims traced
> ```
```

---

## Question Type Guidance

### Phenomenon (`--target-question-type phenomenon`)
- Tests WHETHER an effect exists
- Requires: clear operationalization, measurable outcome
- Testability weighted highest
- Example: "Do specific classifiers amplify mental simulation?"

### Mechanism (`--target-question-type mechanism`)
- Tests HOW or WHY an effect occurs
- Requires: competing theoretical accounts, distinguishing predictions
- Prediction Specificity weighted highest
- Example: "Does amplification occur through profiling or coercion?"

### Boundary (`--target-question-type boundary`)
- Tests WHEN or WHERE an effect applies
- Requires: known phenomenon, moderator variables
- Theoretical Depth weighted highest
- Example: "Does classifier amplification depend on noun animacy?"

### Exploratory (`--target-question-type exploratory`)
- Open-ended investigation
- Lower threshold for prediction specificity
- Theoretical Depth and Provenance weighted highest
- Example: "What cognitive processes underlie classifier selection?"

---

## Quality Standards

### Assessment Quality
- [ ] All 4 criteria evaluated with specific evidence
- [ ] Ratings justified, not arbitrary
- [ ] Gaps are actionable (specific enough to address)
- [ ] Development path provides clear next steps

### Handoff Quality (when PROMOTE)
- [ ] Question formulation is testable
- [ ] Question type matches Thought content
- [ ] Research design hints are feasible
- [ ] Properties template is complete
- [ ] Source links properly traced

### Human Decision Preserved
- [ ] Assessment is recommendation, not mandate
- [ ] Human decides whether to promote
- [ ] Alternative paths suggested if not ready
- [ ] No automatic Question creation

---

## Integration with Other Skills

### Prerequisite:
- **`/thought-provenance-audit`**: Criterion 3 (Provenance Completeness) requires this
- **`/thought-refine`**: Optional but helps with Criterion 2 (Theoretical Depth clarity)

### Downstream:
- **qsp-workflow-manager**: Receives handoff package for Question creation
- **`/thought-question-assess`** may be called again after development

### Cross-agent:
- **connection-workflow-manager**: If assessment reveals Connection gaps, refer upstream

---

## Examples

### Example 1: Mature Thought ready for promotion
```
User: Is my Thought about specific vs general classifiers ready for a Question?

Skill: /thought-question-assess "🤔Specific and general classifiers are distinguished by quantitative or by qualitative aspects"

Output:
- Testability: Ready (clear IV: classifier type, DV: MSE)
- Theoretical Depth: Ready (well-developed Primary Reflection, strong argument)
- Provenance: Ready (8 source links, 90% coverage)
- Prediction Specificity: Ready (quantitative vs qualitative predictions)
- Overall: PROMOTE
- Handoff: Question type = mechanism, suggested title provided
```

### Example 2: Thought needs development
```
User: Can my general classifiers Thought become a Question?

Skill: /thought-question-assess "🤔general classifiers might evoke attention to mental entity"

Output:
- Testability: Developing (MSE effect noted but not formalized)
- Theoretical Depth: Developing (8 lines, sparse arguments)
- Provenance: Not Ready (2 links, below minimum)
- Prediction Specificity: Developing (direction stated, not specific)
- Overall: NEEDS DEVELOPMENT
- Gaps: Add provenance links, deepen Primary Reflection with evidence synthesis
```

### Example 3: Project-generated assessment
```
User: My Project finding about animacy effects — is it Question-worthy?

Skill: /thought-question-assess "🤔animacy finding" --target-question-type boundary

Output:
- Assessment adjusted for boundary question type
- Theoretical Depth weighted highest
- Recommendation: Develop Thought further before Question
```

---

## Related Documentation

- **Question Spec**: `Overview.md` (Question properties, lifecycle)
- **Question Template**: `Templates/Question Template.md`
- **Dashboard**: `ACT/ACT space.md`
- **Related Skills**: `/thought-provenance-audit`, `/thought-refine`

---

## Version History

- **2026-02-13**: Initial creation (Thought Manager Framework Redesign)
- 4-criterion readiness assessment
- Handoff package for qsp-workflow-manager
- Question type guidance (phenomenon/mechanism/boundary/exploratory)
- **2026-02-14**: Strict zettel alignment — updated Theoretical Depth criterion (single Primary Reflection, no multi-Insight), removed status counter reference, updated examples
