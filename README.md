> 繁體中文版：[README.zh-TW.md](README.zh-TW.md)

# ACT_Base

A minimal Obsidian vault demonstrating the **Annotation → Connection → Thought (ACT)** knowledge workflow, powered by Claude Code skills.

Drop in atomic Zettel cards from any paper, run Claude Code skills from a terminal inside Obsidian, and turn isolated cards into a cross-paper knowledge network.

[![Watch Clip 3 — Claude Code annotation demo](https://img.youtube.com/vi/RQa4rl4SYWU/maxresdefault.jpg)](https://youtu.be/RQa4rl4SYWU)

---

## What ACT_Base does

Three knowledge layers, each with dedicated Claude Code skills:

| Layer | Skills |
|-------|--------|
| **Annotation** | `card-review` · `gear-coaching` · `cross-link` · `monitor` |
| **Connection** | `gear-aggregate` · `framework-synthesize` · `query` · `tension-resolve` |
| **Thought** | `provenance-audit` · `refine` · `question-assess` · `question-challenge` |

---

## Prerequisites

1. **Obsidian** — [obsidian.md](https://obsidian.md)
2. **Claude Code** — [claude.ai/code](https://claude.ai/code) (Anthropic account required)
3. **lean-obsidian-terminal** — run Claude Code inside Obsidian: [github.com/sdkasper/lean-obsidian-terminal](https://github.com/sdkasper/lean-obsidian-terminal)
4. **claude_lit_workflow** *(optional, for generating cards from PDFs)* — [github.com/SCgeeker/claude_lit_workflow](https://github.com/SCgeeker/claude_lit_workflow)

---

## Quick Setup

### 1. Clone and open in Obsidian

```bash
git clone https://github.com/SCgeeker/ACT_base.git
```

Open Obsidian → **Open folder as vault** → select the `ACT_base` folder.

### 2. Install lean-obsidian-terminal

Inside Obsidian: **Settings → Community plugins → Browse** → search **lean terminal** → install and enable.

[▶ 01:00 — Install and launch the terminal plugin](https://youtu.be/RQa4rl4SYWU?t=60)

### 3. Open a target Annotation note

Navigate to any note under `ACT/0️⃣Annotation/`. Three demo papers are pre-loaded (`Bengio-2025`, `Borazjanizadeh-2025`, `Shao-2026`).

[▶ 01:16 — Open Annotation note](https://youtu.be/RQa4rl4SYWU?t=76)

### 4. Start Claude Code

Open the lean terminal and run:

```bash
claude
```

[▶ 01:35 — Start Claude Code in Obsidian terminal](https://youtu.be/RQa4rl4SYWU?t=95)

---

## Annotation Skills

Run any skill from the Claude Code terminal. Type `/annotation-` and press Tab to see all options.

### `/annotation-card-review <citekey>`

Weaves 20–30 atomic Zettel cards into a flowing narrative (**Collaborated Annotations**), providing a high-quality starting point for Gear writing. Optionally accepts a `kb_output` path to incorporate Marp slide notes alongside the cards.

```
/annotation-card-review Bengio-2025
/annotation-card-review Bengio-2025 +/kb_output/Bengio-2025/
```

[▶ 02:18 — card-review: 30 cards → narrative draft](https://youtu.be/RQa4rl4SYWU?t=138)

---

### `/annotation-gear-coaching <citekey>`

4-phase human–AI collaboration to distill cross-paper insights into a **Connection Gear** — an English narrative paragraph where every claim links back to a source card.

| Phase | Who | Action |
|-------|-----|--------|
| 1 | AI | Scans cards → proposes 5–7 candidate insights |
| 2 | Human | Selects 2–4 insights, flags research relevance |
| 3 | AI+Human | (Optional) deepening dialogue |
| 4 | AI | Drafts Gear; human reviews card links |

```
/annotation-gear-coaching Bengio-2025
```

[▶ 04:40 — gear-coaching: Phase 1 → insight selection → Gear](https://youtu.be/RQa4rl4SYWU?t=280)

---

### `/annotation-cross-link <citekey>`

Identifies theoretical connections between this paper and other annotations or Connection notes in the vault.

### `/annotation-monitor`

Vault lint scan: reports completion status for all annotations, classifies orphan notes, and outputs an action queue routing unfinished items to the right fix command.

---

## Connection Skills

### `/connection-gear-aggregate`

Aggregates Gears from 3+ annotations to surface synthesis opportunities and plan Connection notes.

```
/connection-gear-aggregate
```

[▶ 10:24 — gear-aggregate: Gears → Connection Note](https://youtu.be/RQa4rl4SYWU?t=624)

Additional connection skills: `connection-framework-synthesize`, `connection-query`, `connection-tension-resolve`.

---

## The ACT Workflow

```
PDF
 └─ claude_lit_workflow → 20–30 atomic Zettel cards
                             │
                    /annotation-card-review
                             │
                    Collaborated Annotations
                             │
                    /annotation-gear-coaching
                             │
                    Connection Gear (English)
                             │
                    /connection-gear-aggregate
                             │
                    Connection Note (cross-paper synthesis)
                             │
                    /thought-* skills → Thought notes → Questions
```

[▶ 13:16 — ACT workflow summary](https://youtu.be/RQa4rl4SYWU?t=796)

---

## Demo Papers

Three pre-loaded annotations are included for exploration. PDFs are not redistributed — fetch them via the DOIs below.

| Citekey | Title | DOI |
|---------|-------|-----|
| Bengio-2025 | Superintelligent Agents Pose Catastrophic Risks: Can Scientist AI Offer a Safer Path? | [10.48550/arXiv.2502.15657](https://doi.org/10.48550/arXiv.2502.15657) |
| Borazjanizadeh-2025 | Modeling Language as a Sequence of Thoughts | [10.48550/arXiv.2512.25026](https://doi.org/10.48550/arXiv.2512.25026) |
| Shao-2026 | SciSciGPT: Advancing Human–AI Collaboration in the Science of Science | [10.1038/s43588-025-00906-6](https://doi.org/10.1038/s43588-025-00906-6) |

---

## License

MIT
