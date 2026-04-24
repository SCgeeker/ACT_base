---
name: thought-refine
description: >
  Improve Thought note writing quality while preserving 100% human voice; integrates P-CSO workflow; checks source link formatting.
  使用時機：Thought 內容已確定但文字品質需要提升、段落連貫性不足、準備投入後續工作流程前的寫作優化。
  觸發詞：「潤飾 Thought」「thought refine」「改善寫作」「Thought 寫作」「文字品質」「改善 Thought」「polish thought」「refine thought」。
  只改善文字表達，不新增任何內容——這是此 skill 的核心限制。
argument-hint: <thought-note-path> [--focus syntax|coherence|links|questions|full]
allowed-tools: Read, Glob, Grep, Edit
user-invocable: true
reusable: false
---

# Thought Refine Skill

Improve Thought note writing quality while preserving 100% human voice and ensuring source link completeness.

---

## Purpose

Enhance the readability and academic quality of human-written Thought notes:

1. **Writing Quality** (P-CSO integration)
   - Sentence-level syntax clarity (Pinker rules)
   - Paragraph-level coherence (topic-comment flow)
   - Academic tone without jargon inflation

2. **Source Link Formatting**
   - Verify all claims have `[[source]]` links
   - Format links consistently: `[[Author-Year-XXX.md|description]]`
   - Ensure links resolve to existing notes

3. **Structural Compliance**
   - Strict zettel: ONE atomic claim per note, developed in single 🧠 Primary Reflection
   - Content migrated from working Connection or Project notes, not written fresh
   - Clear argument structure within the reflection

---

## Critical Constraint

**This skill NEVER adds content to Thought notes.**

- Only improves existing human-written text
- May suggest where source links should be added (but human adds them)
- May rephrase for clarity (but preserves the human's argument)
- If content gaps exist, flag them for human attention — do not fill them

---

## Input

The target note can be specified using `@path` syntax or quoted title.

### Mode 1: Full Refinement
```
/thought-refine @"ACT\2️⃣Thought\🤔general classifiers might evoke attention to mental entity.md"
/thought-refine "🤔general classifiers might evoke attention to mental entity"
```
Apply all refinement passes: syntax, coherence, links, questions, structure.

### Mode 2: Focused Refinement
```
/thought-refine @"ACT\2️⃣Thought\🤔xxx.md" --focus syntax
/thought-refine @"ACT\2️⃣Thought\🤔xxx.md" --focus questions
```
Options:
- `syntax`: Sentence-level clarity (Pinker Chapter 4 rules)
- `coherence`: Paragraph flow and topic continuity (Pinker Chapter 5)
- `links`: Source link formatting and completeness only
- `questions`: Question-aware checks only (Rationale blocks, transclusion, scope map)
- `full`: All passes (default)

---

## Workflow

### Step 1: Read and Assess
```
1. Read Thought note content
2. Check if /thought-provenance-audit has been run first
   - If yes: Use provenance table to guide link suggestions
   - If no: Flag that provenance audit is recommended first
3. Assess current quality:
   - Primary Reflection coherence and depth
   - Source link count
   - Atomicity check (one claim per note)
```

### Step 2: Syntax Pass (if --focus includes syntax)
```
Apply Pinker's 6 sentence-level rules:
1. Avoid left-branching structures
2. Minimize passive voice (unless justified)
3. Reduce nominalizations
4. Keep subject-verb-object close together
5. Avoid garden-path ambiguity
6. Use parallel structure in lists

Clause-structure conventions (user-confirmed):
7. Do NOT use em-dashes (—) to connect clauses; split into separate sentences or use explicit connectives ("This manipulation produced," "including," "because")
8. Do NOT use parentheses for inline lists; use "including X, Y, and Z" or comma-delimited appositive clauses
9. Do NOT use relative clauses (which/that/who); convert to separate sentences
10. Do NOT use subordinate clauses where a direct sentence works; prefer Subject-Verb-Object pattern

For each suggestion:
- Quote original sentence
- Provide refined version
- Explain which rule applies
- Human approves before applying
```

### Step 3: Coherence Pass (if --focus includes coherence)
```
Apply Pinker's 7 discourse-level principles:
1. Clear topic sentence for each section
2. Given-before-new information flow
3. Consistent topic string across sentences
4. Explicit connectives where needed
5. Avoid abrupt topic shifts
6. Paragraph unity (one main idea)
7. Smooth transitions between sections
```

### Step 4: Link Pass (if --focus includes links)
```
1. Identify all assertions/claims in text
2. Check each has a [[source]] link
3. Verify link format:
   - Annotation: [[Author-Year-XXX.md|description]] or [[@Author-Year]]
   - Connection: [[🔗Title]]
   - Thought: [[🤔Title]]
4. Check links resolve (file exists)
5. Count total links vs minimum (3-7)
6. Verify inner link format for migrated content:
   - Connection heading links: [[🤔Thought title|Section Heading]]
   - Title must match Thought note title exactly
   - Flag mismatches between inner link target and actual Thought note name
```

### Step 4.5: Question-Aware Pass (if --focus includes questions)

**Trigger condition**: Thought note has non-empty `question:` frontmatter field.

If `question:` is empty (`-`), skip this pass entirely.

**4.5a: Rationale Block Quality Check**
```
For each Question in the question: field:
1. Find the corresponding Rationale block in "🎯 Questions Upgraded" section
2. Identify the ^blockid (e.g., ^71efc0)
3. Classify Rationale content:
   - DESCRIPTIVE: Only describes what was found (e.g., "Study X compared A and B")
   - GENERATIVE: Explains WHY this finding generates a Question
     (e.g., "...but causal direction remains untested")
4. If DESCRIPTIVE only:
   ⚠️ Flag: "Rationale block ^blockid is descriptive (WHAT) but lacks
   generative narrative (WHY this creates a Question). This block is
   transcluded into Question Origin — expanding it here improves
   Question Origin automatically."
5. Add TODO(human) memo under the block if gap found
```

**4.5b: Transclusion Placement Advisory**
```
For each Question in the question: field:
1. Read the Question note
2. Check if any ^blockid from this Thought is transcluded (![[...#^blockid]])
3. Check WHERE the transclusion appears:
   - In WH section → ⚠️ "Block ^blockid is rationale content but is
     transcluded in WH (prediction) section. Consider moving to Origin."
   - In Origin section → ✓ Correct placement
   - Not transcluded → Note: "No transclusion found"
```

**4.5c: Topic-Level Title Detection (upstream prevention)**
```
For each Question in the question: field:
1. Read the Question title
2. Check if title uses topic-level framing:
   - "What are the X for Y" → ⚠️ TOPIC-LEVEL
   - "What kind of X" → ⚠️ TOPIC-LEVEL
   - "Does/Do/Can/How" → ✓ TESTABLE framing
3. If TOPIC-LEVEL detected:
   ⚠️ "Question title uses topic-level framing. Check if Rationale
   block includes a testable prediction direction — if not, downstream
   Questions tend to inherit topic-level framing."
   Suggest: /question-scope-sharpen on the Question note
```

**4.5d: Question-Thought Scope Map**
```
Generate summary table:
| Question | Scope Relation | Alignment |
|---|---|---|
| [Q title] | Thought → [causal/structural/boundary] test | [✓/⚠️] |

This is informational — helps human see how Questions relate to the Thought.
```

### Step 5: Generate Refinement Report
```markdown
## Refinement Report: 🤔[Title]
**Generated**: YYYY-MM-DD
**Focus**: [syntax|coherence|links|full]

### Summary
- Syntax issues found: N
- Coherence issues found: M
- Link issues found: P
- Question-aware issues found: Q (or "N/A — no linked Questions")
- Structural compliance: PASS/FAIL

### Suggested Edits
[Numbered list of specific edit suggestions with before/after]

### Link Gaps
[Claims needing source links]

### Question-Aware Checks (if question: field is non-empty)
[Rationale block quality, transclusion placement, topic-level detection, scope map]

### Human Decision Required
[Items where multiple valid options exist]
```

---

## Output Format

### Edit Suggestions (presented for human approval)
```markdown
### Edit #1 (Syntax: reduce nominalization)
**Original**: "The null effect with general classifiers suggests they fail to activate the detailed perceptual representations necessary for mental simulation"
**Refined**: "General classifiers fail to activate the detailed perceptual representations that mental simulation requires, as shown by the null effect"
**Rule**: SVO proximity + active voice
**Accept?**: [ ] Yes [ ] No [ ] Modify
```

### Link Suggestions
```markdown
### Link #1
**Claim**: "general classifiers (如'個') lack the semantic specificity to profile particular object features"
**Missing link**: Needs source for "semantic specificity" claim
**Suggested**: `[[Wu-2020|profiling hypothesis]]` or `[[Zhang-2013-ch07-008|CL_u semantic vacuity]]`
**From provenance audit**: Line 81 of 🔗Linguistic theories
```

---

## Quality Standards

### Writing Quality
- [ ] No sentences exceed 40 words without good reason
- [ ] Active voice used where possible
- [ ] Technical terms defined or linked on first use
- [ ] Parallel structure in comparative claims
- [ ] No em-dashes (—) used for clause connection
- [ ] No parentheses used for inline lists
- [ ] No relative clauses (which/that/who); converted to separate sentences
- [ ] No subordinate clauses where a direct sentence suffices

### Source Links
- [ ] 3-7 total links minimum (THE FIRST RULE)
- [ ] Format consistent across note
- [ ] All links resolve to existing files
- [ ] Key claims have specific card links (not just note-level)

### Question-Aware Quality (when question: field is non-empty)
- [ ] Rationale blocks classified (DESCRIPTIVE vs GENERATIVE)
- [ ] DESCRIPTIVE-only blocks flagged with TODO(human) memo
- [ ] Transclusion placement checked in downstream Question notes
- [ ] Topic-level Question titles flagged with /question-scope-sharpen suggestion
- [ ] Scope map generated for all linked Questions

### Human Voice Preservation
- [ ] Arguments unchanged in substance
- [ ] Only expression improved, not content
- [ ] Human's distinctive phrasing preserved where it serves clarity
- [ ] No new claims or evidence introduced

---

## Integration with Other Skills

### Prerequisite:
- **`/thought-provenance-audit`**: Should run first to establish what sources should be linked

### Downstream:
- **`/thought-question-assess`**: Refined Thought is better candidate for assessment

### Parallel:
- **`/pinker-syntax`**: Sentence-level rules (can be called independently)
- **`/pinker-coherence`**: Paragraph-level rules (can be called independently)
- **`/p-cso-workflow`**: Full pipeline (syntax + coherence combined)

---

## Examples

### Example 1: Full refinement
```
User: Please refine my general classifiers Thought note.

Skill: /thought-refine "🤔general classifiers might evoke attention to mental entity"

Output:
- 3 syntax suggestions (reduce nominalizations, improve SVO)
- 1 coherence suggestion (topic string continuity)
- 4 link gaps identified (needs [[Wu-2020]], [[Zhang-2013-ch07]])
- Structural: 1 section exceeds 5-sentence limit
```

### Example 2: Links only
```
User: Just check the source links in my Thought note.

Skill: /thought-refine "🤔xxx" --focus links

Output:
- 5 assertions found, 2 with links, 3 without
- Total links: 2 (minimum 3-7: BELOW MINIMUM)
- 3 specific link suggestions from provenance audit
```

### Example 3: Question-aware refinement
```
User: /thought-refine @"ACT\2️⃣Thought\🤔Most animal nouns occupy mid-to-low profiling strength range.md"

Skill detects: question: field has 2 linked Questions

Output:
- 2 syntax edits (grammar, dangling participle)
- 1 coherence edit (demonstrative pronoun)
- Question-Aware Checks:
  - ^71efc0: DESCRIPTIVE only — missing WHY this generates Q1
  - ^15c55f: DESCRIPTIVE only — missing WHY this generates Q2
  - Q1 transclusion in WH section → advisory to move to Origin
  - Q2 transclusion in WH section → advisory to move to Origin
  - Both Q titles were topic-level → /question-scope-sharpen suggested
  - Scope map: Q1=causal test, Q2=structural test (complementary)
```

### Example 4: Question-focused only
```
User: /thought-refine @"ACT\2️⃣Thought\🤔xxx.md" --focus questions

Output:
- Skips syntax/coherence/links passes
- Only runs Step 4.5: Question-Aware Pass
- Reports Rationale quality, transclusion placement, scope map
```

---

## Related Documentation

- **P-CSO Framework**: `/p-cso-workflow`, `/pinker-syntax`, `/pinker-coherence`
- **Dashboard**: `ACT/ACT space.md`
- **Spec**: `Overview.md` (spec point 8: 100% human, spec point 9: AI checks links)
- **Related Skills**: `/thought-provenance-audit`, `/thought-question-assess`

---

## Version History

- **2026-02-13**: Initial creation (Thought Manager Framework Redesign)
- Writing enhancement skill with P-CSO integration
- Strict human-voice preservation constraint
- Depends on provenance audit for source link guidance
- **2026-02-13b**: Added inner link format validation for migrated content (Connection heading → Thought section matching)
- **2026-02-14**: Strict zettel alignment — updated structural compliance (single Primary Reflection, atomicity), inner link format (note-level, no `#Insight N`)
- **2026-02-24**: Clause-structure conventions (from session work on Q-paradigm and Q-ERP-confound)
  - Rule 7: No em-dashes (—) for clause connection; use periods or explicit connectives
  - Rule 8: No parentheses for inline lists; use "including X, Y, and Z" pattern
  - Added to Syntax Pass rules and Writing Quality checklist
- **2026-02-20**: Question-Aware Pass (Step 4.5) — iterated from session work on 🤔Most animal nouns
  - 4.5a: Rationale block quality (DESCRIPTIVE vs GENERATIVE classification)
  - 4.5b: Transclusion placement advisory (WH vs Origin section check)
  - 4.5c: Topic-level title detection (upstream prevention for Question scope issues)
  - 4.5d: Question-Thought scope map (informational alignment table)
  - New `--focus questions` option for Question-aware checks only
  - Updated input format: accepts `@path` syntax for target note specification
