# ACT_Base

極簡的 Obsidian vault，透過 Claude Code skills 示範 **Annotation → Connection → Thought（ACT）** 知識工作流程。

將論文的原子 Zettel 卡片匯入後，在 Obsidian 內的終端機執行 Claude Code skills，將零散卡片轉化為跨論文知識網絡。

[![觀看 Clip 3 — Claude Code annotation 互動示範](https://img.youtube.com/vi/RQa4rl4SYWU/maxresdefault.jpg)](https://youtu.be/RQa4rl4SYWU)

---

## ACT_Base 能做什麼

三個知識層，各有對應的 Claude Code skills：

| 層級 | Skills |
|------|--------|
| **Annotation** | `card-review` · `gear-coaching` · `cross-link` · `monitor` |
| **Connection** | `gear-aggregate` · `framework-synthesize` · `query` · `tension-resolve` |
| **Thought** | `provenance-audit` · `refine` · `question-assess` · `question-challenge` |

---

## 前置需求

1. **Obsidian** — [obsidian.md](https://obsidian.md)
2. **Claude Code** — [claude.ai/code](https://claude.ai/code)（需要 Anthropic 帳號）
3. **lean-obsidian-terminal** — 在 Obsidian 內執行 Claude Code：[github.com/sdkasper/lean-obsidian-terminal](https://github.com/sdkasper/lean-obsidian-terminal)
4. **claude_lit_workflow** *（選用，用於從 PDF 生成原子卡片）* — [github.com/SCgeeker/claude_lit_workflow](https://github.com/SCgeeker/claude_lit_workflow)

---

## 快速設定

### 1. Clone 並以 Obsidian 開啟

```bash
git clone https://github.com/SCgeeker/ACT_base.git
```

開啟 Obsidian → **以資料夾開啟 vault** → 選取 `ACT_base` 資料夾。

### 2. 安裝 lean-obsidian-terminal

在 Obsidian 內：**設定 → 社群插件 → 瀏覽** → 搜尋 **lean terminal** → 安裝並啟用。

[▶ 01:00 — 安裝並啟動 terminal 外掛](https://youtu.be/RQa4rl4SYWU?t=60)

### 3. 開啟目標 Annotation note

前往 `ACT/0️⃣Annotation/` 下的任一筆記。vault 已預載三篇示範論文（`Bengio-2025`、`Borazjanizadeh-2025`、`Shao-2026`）。

[▶ 01:16 — 開啟 Annotation note](https://youtu.be/RQa4rl4SYWU?t=76)

### 4. 啟動 Claude Code

開啟 lean terminal 並執行：

```bash
claude
```

[▶ 01:35 — 在 Obsidian terminal 啟動 Claude Code](https://youtu.be/RQa4rl4SYWU?t=95)

---

## Annotation Skills

在 Claude Code terminal 輸入 `/annotation-` 後按 Tab，可查看所有選項。

### `/annotation-card-review <citekey>`

將 20–30 張原子 Zettel 卡片編織成流暢學術敘事（**Collaborated Annotations**），作為撰寫 Connection Gear 的高品質起點。可附加 `kb_output` 路徑，將 Marp 投影片筆記一併融入敘事。

```
/annotation-card-review Bengio-2025
/annotation-card-review Bengio-2025 +/kb_output/Bengio-2025/
```

[▶ 02:18 — card-review：30 張卡片 → 流暢敘事草稿](https://youtu.be/RQa4rl4SYWU?t=138)

---

### `/annotation-gear-coaching <citekey>`

4 階段人機協作循環，從卡片提煉跨論文洞見，組裝出 **Connection Gear**——每個主張連結來源卡片的英文敘事段落。

| 階段 | 執行者 | 動作 |
|------|--------|------|
| 1 | AI | 掃描卡片 → 提出 5–7 個候選洞見 |
| 2 | Human | 選擇 2–4 個洞見，標記研究相關性 |
| 3 | AI+Human | （選用）深化對話 |
| 4 | AI | 撰寫 Gear 草稿；Human 審閱卡片連結 |

```
/annotation-gear-coaching Bengio-2025
```

[▶ 04:40 — gear-coaching：Phase 1 → 選擇洞見 → 完成 Gear](https://youtu.be/RQa4rl4SYWU?t=280)

---

### `/annotation-cross-link <citekey>`

識別此論文與 vault 中其他 annotations 或 Connection notes 的理論連結機會，建立跨文獻網絡。

### `/annotation-monitor`

Vault lint 掃描：回報所有 annotations 的完成狀態，分類孤兒筆記，輸出 Action Queue 並路由至對應的修復指令。

---

## Connection Skills

### `/connection-gear-aggregate`

聚合 3+ 篇論文的 Annotation Gears，識別跨文獻主題與 Connection note 發展機會。

```
/connection-gear-aggregate
```

[▶ 10:24 — gear-aggregate：Gears → Connection Note](https://youtu.be/RQa4rl4SYWU?t=624)

其他 connection skills：`connection-framework-synthesize`、`connection-query`、`connection-tension-resolve`。

---

## ACT 工作流程

```
PDF
 └─ claude_lit_workflow → 20–30 張原子 Zettel 卡片
                             │
                    /annotation-card-review
                             │
                    Collaborated Annotations（中文敘事）
                             │
                    /annotation-gear-coaching
                             │
                    Connection Gear（英文，附卡片連結）
                             │
                    /connection-gear-aggregate
                             │
                    Connection Note（跨論文綜合）
                             │
                    /thought-* skills → Thought notes → 研究問題
```

[▶ 13:16 — ACT workflow 小結](https://youtu.be/RQa4rl4SYWU?t=796)

---

## 示範論文

Vault 預載三篇 Annotation 供探索。PDF 不隨 repo 發佈，請透過以下 DOI 自行取得。

| Citekey | 標題 | DOI |
|---------|------|-----|
| Bengio-2025 | Superintelligent Agents Pose Catastrophic Risks: Can Scientist AI Offer a Safer Path? | [10.48550/arXiv.2502.15657](https://doi.org/10.48550/arXiv.2502.15657) |
| Borazjanizadeh-2025 | Modeling Language as a Sequence of Thoughts | [10.48550/arXiv.2512.25026](https://doi.org/10.48550/arXiv.2512.25026) |
| Shao-2026 | SciSciGPT: Advancing Human–AI Collaboration in the Science of Science | [10.1038/s43588-025-00906-6](https://doi.org/10.1038/s43588-025-00906-6) |

---

## 授權

MIT
