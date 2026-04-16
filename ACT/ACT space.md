---
aliases:
  - ACT Space
  - Knowledge Base
tags:
  - dashboard
---

# 🧠 ACT Space — Active Content & Thoughts

> [!abstract]+ System Overview
> **Entry Point** to all knowledge accumulation in this vault.
>
> **Knowledge Pipeline**: Raw PDFs → **Annotations** → **Connections** → **Thoughts**
>
> - **Annotations**: Compiled paper summaries with 20 atomic zettel cards + Connection Gear
> - **Connections**: Cross-paper concept synthesis (Map of Content for ACT)
> - **Thoughts**: Emerged atomic theoretical claims
>
> **Lint**: `/annotation-monitor` — scan orphans, old-style backlog, concept gaps
> **Query**: `/connection-query` — ask questions against this knowledge base, file answers back
>
> For Knowledge Index (bottom of this file):
> - Updated by LLM after each Gear completion, Connection update, or Thought emergence
> - One-line per note: serves as the index layer for efficient `/connection-query` navigation

---

## 📊 ACT Analytics

> [!summary]- Quick Stats
> - **Total Annotations**: `$= dv.pages('"ACT/0️⃣Annotation"').where(p => p.tags == "concept/anno").length`
> - **Gear Completed**: `$= dv.pages('"ACT/0️⃣Annotation"').where(p => p.geared === true).length`
> - **Connection Notes**: `$= dv.pages('"ACT/1️⃣Conn"').where(p => p.tags == "concept/conn").length`
> - **Thought Notes**: `$= dv.pages('"ACT/2️⃣Thought"').where(p => p.tags == "concept/thought").length`

---

## 📚 Annotation Status

> [!info]- Status Legend
> - ✅ Annotated + Geared + Connected — fully integrated
> - 🔄 Annotated + Geared — awaiting Connection
> - ⬜ Annotated only — Gear pending
> - 🟥 Not yet annotated

![[Notes.base#Annotations]]

---

## 🔗 Connection Notes

![[Notes.base#Connections]]

---

## 🤔 Thought Notes

![[Notes.base#Thoughts]]

---

## 🗂 Knowledge Index

<!-- LLM-MAINTAINED SECTION -->
<!-- Update protocol:
     - After /annotation-gear-coaching Phase 4 → add/update one line under Annotations
     - After Connection note status update → update one line under Connections
     - After Thought note creation → add one line under Thoughts

     FORMAT SPEC:
     Annotations : - [[Author-Year]] ⟶ [[🔗Connection]] — [Gear key claim, one sentence]
     Connections : - [[🔗Title]] — status:[N] | 🟢[X] 🟡[Y] 🧩[Z] | [core tension or synthesis stance]
     Thoughts    : - [[🤔Title]] [🟢/🟡/🧩] — (from [[🔗Connection]])
                   Note: Thought title IS the atomic claim — no paraphrase needed -->

### Annotations

### Connections

### Thoughts

---

## 🔍 Navigation

Lint: `/annotation-monitor` | Query: `/connection-query`
