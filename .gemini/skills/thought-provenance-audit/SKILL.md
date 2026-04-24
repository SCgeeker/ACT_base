---
name: thought-provenance-audit
description: >
  Trace Thought note claims to specific source paragraphs in Connection or Project notes, strengthening provenance from note-level to paragraph-level.
  使用時機：Thought 完成後進行品質審查、論點來源模糊、準備升格為 Question 之前的溯源驗證。
  觸發詞：「溯源」「provenance audit」「核實來源」「Thought 審查」「找出處」「段落溯源」「追蹤來源」「trace claims」「哪裡支持」。
  Thought 完成後應主動建議使用此 skill，確保段落層級溯源完整再進行下一步。
argument-hint: <thought-note-path> [--source <connection-or-project-path>] [--mode pre-migration|post-creation|project-findings]
allowed-tools: Read, Glob, Grep, Write, Edit
user-invocable: true
reusable: true
---

# Thought Provenance Audit Skill

Trace Thought note claims to specific source paragraphs. The core traceability mechanism for the Thought layer.

---

## Purpose

Map every claim in a Thought note to its source paragraph in Connection or Project notes, producing a **Provenance Table** as a working document.

1. **Provenance Table** (core output)
   - Claim -> source paragraph mapping
   - Line references for traceability
   - Coverage assessment (orphaned claims / orphaned evidence)

2. **Gap Report** (when auditing existing notes)
   - Claims without source links
   - Sources cited but not used in arguments
   - THE FIRST RULE compliance score

3. **Pattern Map** (Route B: Project findings)
   - Project findings -> emergent theoretical patterns
   - Candidate Question identification
   - Existing Thought home suggestions

---

## Input

### Mode 1: Pre-Migration Analysis (Connection -> Thought)
```
/thought-provenance-audit "🤔general classifiers might evoke attention to mental entity" --source "🔗Cognitive functions of sortal classifiers" --mode pre-migration
```
Scan Connection note for paragraphs consistent with existing or planned Thought claims.

### Mode 2: Post-Creation Validation
```
/thought-provenance-audit "🤔general classifiers might evoke attention to mental entity"
```
Auto-detect parent Connection(s) from frontmatter, validate all claims have paragraph-level sources.

### Mode 3: Project Findings Mapping (Route B)
```
/thought-provenance-audit --source "🧪Investigate Amplification Mechanism" --mode project-findings
```
Map Project findings to emergent patterns, suggest Thought homes or new Question candidates.

### Mode 4: Post-Migration Validation
```
/thought-provenance-audit "🤔general classifiers might evoke attention to mental entity" --mode post-migration
```
Validate BOTH sides of a completed Connection→Thought content migration:
- **Thought side**: Primary Reflection contains migrated evidence with source links, provenance chain intact
- **Connection side**: Section heading is inner link to Thought note, content replaced with `[!thought]` callout
- **Inner link format**: `[[🤔Thought title|Section Heading]]` — title must match Thought note exactly
- **Atomicity check**: Flag if Thought note accumulates multiple independent ideas (should split)

---

## Workflow

### Step 1: Source Identification
```
1. Read target Thought note (if exists)
2. Identify parent sources:
   - Route A: Identify parent Connection from body source links or user input
   - Route B: Read origin_source: property -> load Project note(s)
3. If --source specified, use that instead
4. Extract all claims from Thought note (each sentence/assertion)
```

### Step 2: Source Paragraph Scanning
```
For each parent Connection/Project note:
1. Identify all H3/H4 subsections with line numbers
2. For each subsection, extract key claims and evidence
3. Build paragraph-level index:
   - Line range: X-Y
   - Section title
   - Key claims (1-2 sentence summary)
   - Source annotations cited
```

### Step 3: Claim-Source Mapping
```
For each claim in the Thought note:
1. Search parent notes for consistent paragraphs
2. Rate consistency:
   - DIRECT: Paragraph directly states this claim
   - SUPPORTS: Paragraph provides evidence for this claim
   - RELATED: Paragraph discusses related topic
   - NONE: No corresponding source found
3. Record mapping with line references
```

### Step 4: Generate Provenance Table
```markdown
## Provenance Table: 🤔[Thought Title]
**Generated**: YYYY-MM-DD
**Source(s)**: [[🔗Connection]] / [[🧪Project]]

| # | Claim (from Thought) | Source Note | Line(s) | Section | Consistency | Source Annotations |
|---|---|---|---|---|---|---|
| 1 | [claim text] | 🔗Connection | 81-83 | CL_u Analysis | DIRECT | [[Zhang-2013-ch07]] |
| 2 | [claim text] | 🔗Connection | 43 | Profiling | SUPPORTS | [[Wu-2020]] |
| 3 | [claim text] | — | — | — | NONE | — |
```

### Step 5: Post-Migration Validation (Mode 4 only)
```
For each migrated section:
1. Read Connection note, find sections with [[🤔...]] inner link headings
2. Verify inner link target matches Thought note title exactly
   - Format: [[🤔Thought title|Original Section Heading]]
3. Verify Connection section has [!thought] callout (not raw content)
4. Read corresponding Thought note, verify Primary Reflection contains migrated content
5. Atomicity check:
   - Does Thought note contain multiple independent ideas?
   - If yes → flag for splitting into separate Thought notes
```

### Step 6: Coverage Assessment
```markdown
## Coverage Assessment

**Provenance Score**: X/Y claims mapped (Z%)

### Orphaned Claims (claims without sources)
- Claim #3: "[text]" — needs source or removal

### Orphaned Evidence (sources not used in arguments)
- [[🔗Connection]] Line 75 (Yi-2009 grammaticalized "one") — relevant but not cited

### THE FIRST RULE Compliance
- Total source links: N (minimum: 3-7)
- Paragraph-level references: M
- Note-level only: P
- Status: PASS / NEEDS IMPROVEMENT
```

---

## Output

### Standard Output: Provenance Report

```markdown
# Provenance Audit: 🤔[Thought Title]
**Generated**: YYYY-MM-DD
**Mode**: [pre-migration | post-creation | project-findings]
**Source(s)**: [[source notes]]

---

## Provenance Table

[Table as in Step 4]

---

## Coverage Assessment

[Assessment as in Step 5]

---

## Recommendations

### For Human Action:
1. [Specific recommendation with line references]
2. [Source to add for uncovered claim]

### Source Link Suggestions:
- Claim #1 -> add `[[Zhang-2013-ch07-008|CL_u as placeholder]]`
- Claim #2 -> add `[[Wu-2020|profiling hypothesis]]`

### Next Steps:
- [ ] Human reviews and accepts/rejects mappings
- [ ] Human adds missing source links
- [ ] Run /thought-refine after provenance is complete
```

---

## Quality Standards

### Provenance Table
- [ ] Every Thought claim has a mapping entry
- [ ] Line references are accurate (verified by reading source)
- [ ] Consistency ratings are justified
- [ ] Source annotations identified for each mapping

### Coverage Assessment
- [ ] Orphaned claims identified with specific text
- [ ] Orphaned evidence identified with line references
- [ ] THE FIRST RULE score calculated
- [ ] Actionable recommendations provided

### Human Boundary
- [ ] Audit reports mapping, NOT generating Thought content
- [ ] Recommendations frame as "suggestions for human review"
- [ ] No claims added to Thought note without human approval

---

## Reusability

### 1. Thought Notes (ACT/2️⃣Thought/) - Primary
- Pre-migration analysis for Connection -> Thought workflow
- Post-creation validation for existing Thoughts
- Ongoing audit for spec compliance

### 2. Further Research (downstream)
- Map Thought claims to potential research questions
- Identify theoretical insights needing further exploration
- Track evidence chains from annotations to theory

---

## Integration with Other Skills

### Within thought-workflow-manager:
- **Upstream of `/thought-refine`**: Provenance audit identifies what sources should be linked before writing refinement
- **Upstream of `/thought-question-assess`**: Provenance completeness is a readiness criterion

### Cross-agent:
- **`/connection-framework-synthesize`**: Framework synthesis output feeds provenance mapping
- **`/connection-tension-resolve`**: Tension resolution provides theoretical claims to trace

---

## Examples

### Example 1: Audit existing Thought against Connections
```
User: Can you trace the claims in my general classifiers Thought?

Skill: /thought-provenance-audit "🤔general classifiers might evoke attention to mental entity"

Output:
- 5 claims identified in Thought note
- 3 mapped to 🔗Cognitive functions (Lines 97-131)
- 2 mapped to 🔗Linguistic theories (Lines 75, 81-83)
- 0 orphaned claims
- THE FIRST RULE: 2/7 minimum (NEEDS IMPROVEMENT)
```

### Example 2: Pre-migration for Connection subsection
```
User: I want to migrate the "Distributed Individuation" section into a Thought.

Skill: /thought-provenance-audit --source "🔗Linguistic theories" --mode pre-migration

Output:
- Section spans Lines 87-112
- 6 candidate claims identified
- 4 testable predictions found
- Source annotations: Yi-2009, Zhang-2007, Zhang-2013-ch07
- Recommendation: Mature enough for Thought extraction
```

### Example 3: Project findings mapping (Route B)
```
User: My Classifier Amplification study has new findings. Where do they fit?

Skill: /thought-provenance-audit --source "🧪Investigate Amplification Mechanism" --mode project-findings

Output:
- 3 findings mapped to existing Thoughts
- Finding: "null MSE for general CL" -> 🤔general classifiers
- 1 finding suggests new Question candidate
- Recommendation: Update existing Thought, formulate new Question
```

### Example 4: Post-migration validation
```
User: I moved the profiling evidence from my Connection into the Thought Insight. Can you verify?

Skill: /thought-provenance-audit "🤔general classifiers might evoke attention to mental entity" --mode post-migration

Output:
- Thought side: Primary Reflection contains migrated evidence ✓
- Connection side: Heading is inner link [[🤔Thought title|Section Heading]] ✓
- Inner link format: matches Thought note title exactly ✓
- [!thought] callout present with summary link ✓
- Atomicity check: PASS (one atomic claim per note)
```

---

## Troubleshooting

### Issue 1: Connection note too long for complete scan
**Solution**: Focus on H3/H4 sections most relevant to the Thought's title/claims. Use Grep to locate specific terms.

### Issue 2: Claim spans multiple source paragraphs
**Solution**: Map to primary source (DIRECT) and list secondary sources (SUPPORTS). Record all line references.

### Issue 3: Thought predates Connection content
**Solution**: Some older Thoughts may have content that was later integrated into Connections. Map bidirectionally and flag for human review.

---

## Related Documentation

- **Dashboard**: `ACT/ACT space.md`
- **Template**: `Templates/Template, Thought Note, from Connections.md`
- **Related Skills**: `/thought-refine`, `/thought-question-assess`

---

## Version History

- **2026-02-13**: Initial creation (Thought Manager Framework Redesign)
- Core skill of thought-workflow-manager 3-skill architecture
- Supports Route A (Connection->Thought) and Route B (Project->Thought)
- Paragraph-level provenance strengthens THE FIRST RULE
- **2026-02-14**: Strict zettel alignment — removed Insight references, updated inner link format, atomicity check replaces splitting assessment
- **2026-02-13b**: Added Mode 4 (post-migration validation), splitting assessment, Example 4
