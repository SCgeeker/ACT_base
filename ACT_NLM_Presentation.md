---
theme: default
paginate: true
---

# 🧠 擁抱 AI 流暢度：重塑個人知識管理
### ACT 系統與 LLM-wiki 的深度整合架構

---

## AI Fluency（AI 流暢度）

根據 [Anthropic Skilljar 課程](https://anthropic.skilljar.com/)，當代知識工作者必須將 AI 融入核心工作流。

我們不再只是「搜尋」知識，而是學習如何指揮 AI 進行：

- **消化**：快速掌握文獻全局，不被資訊量淹沒
- **結構化**：原子化拆解與跨文獻連結
- **再創造**：從連結中萃取原創理論主張

這份指南帶您探索如何將傳統卡片盒筆記與最新 LLM 架構整合。

---

# 一：兩種知識管理典範

現代知識管理存在兩條截然不同的路徑。

---

## 🔹 ACT：由下而上（Bottom-Up）

**[Annotation → Connection → Thought](https://www.youtube.com/watch?v=ktukNk2jfhA&list=PLSxoRcsvTAqAb05Kxp-B_FgccZbwTyFLX)**

| 階段 | 操作 | 工具 |
|------|------|------|
| 原子化 | PDF → 20-30 張 Zettel 卡片 | `claude_lit_workflow` |
| 敘事化 | 卡片 → 流動敘事草稿 | `/annotation-card-review` |
| 提煉 | 敘事 → Connection Gear（英文）| `/annotation-gear-coaching` |
| 合成 | 多篇 Gear → Connection Notes | `/connection-gear-aggregate` |
| 主張 | Connection → Thought Notes | `/thought-refine` |

- **優勢**：連結深、主張可溯源至段落級來源
- **劣勢**：必須完整精讀一篇文獻才能啟動流程，前期認知成本高

---

## 🔄 逆向ACT 的可行性

傳統 ACT 假設你**從原子出發**（A→C→T）。
但整理研究文獻過程，我們也可以反過來做：

```
TCA（由上而下）：
Thought（全局觀）──► Connection（框架辨識）──► Annotation（深潛）
```

**為什麼 TCA 有可行性？**
- 進入新領域時，先有地圖再深潛更符合自然認知流
- 可先辨識哪些文獻值得精讀，再投入時間

**為什麼直接實作TCA 很罩門？**
- 「Thought」若無來源支撐 → 只是印象，非知識
- 缺乏原子化連結 → 無法驗證主張、難以反駁

> **核心問題**：有沒有辦法讓 TCA 的全局觀與 ACT 的嚴謹性同時存在？

---

## 🔹 LLM-Wiki：Karpathy 的三層架構

Andrej Karpathy（2025）提出：知識應**一次編譯、持續維護**，而非每次查詢時重新推導。

```
┌──────────────────────────────────────────┐
│  raw/       原始文獻（不可變，持續 Ingest）│
│  wiki/      AI 編譯的結構化概念頁面        │ ← 持續更新
│  schema     維護規則與品質標準             │
└──────────────────────────────────────────┘
```

> "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase."
> — Andrej Karpathy

**核心差異**：
- **RAG**：無狀態，每次查詢重新檢索，知識不累積
- **LLM-Wiki**：有狀態，知識持續複利累積，每篇新文獻改善所有既有 context

---

## 🔹 LLM-Wiki：三個核心操作

| 操作         | 功能                             | 軟體工程類比         |
| ---------- | ------------------------------ | -------------- |
| **Ingest** | 讀入新文獻 → AI 提取概念 → 自動更新頁面與交叉連結  | `git commit`   |
| **Query**  | 對知識庫提問 → 從 wiki 回答 → 結果存回 wiki | `git log`      |
| **Lint**   | 健康檢查：矛盾、孤兒概念、過時資訊              | CI/CD pipeline |

**規模能力**：可處理 100 篇文獻（約 400K 字）的跨文獻即時對話

*(來源：[Karpathy 原版](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)、[張維峰評論](https://www.facebook.com/jerry.chang.505523/posts/pfbid06G7b8aTzU7wTfb8q4nrrcd3wmbSoUnqqXxYf3BfAcHkTQQPfHotN3oBwgwES4Fpw)、[fu_liren 學習心得](https://www.threads.com/@fu_liren.ai/post/DXH4Cz4E9JY?xmt=AQF0b6OTwnt8f_m2cNTNuhpgYsLBEjUfp0HJzzSL0VDqug))*

---

## ⚠️ LLM-Wiki 的已知問題

**1. Container Boundary 問題**（WenHao Yu, 2026）
每個概念要放到哪個 wiki 頁面？邊界模糊。
Zettelkasten 的解法：原子概念 + 連結，繞過邊界決策。

**2. Model Collapse 風險**（WenHao Yu, 2026）
LLM 讀取自己的摘要 + 新資料 → 反覆壓縮 → 資訊退化。
越成熟的知識庫，AI 越依賴自己的輸出。

**3. Vibe Thinking 陷阱**
外包「整理」而非「思考」？若連結由 AI 產生而非人類理解，深度從何而來？

**# Rohit Ghumare（2026）的 v2 迭代**：
信心分數 × 遺忘曲線 × 知識圖譜分層 × 混合搜尋

*(來源：[LLM Wiki v2](https://gist.github.com/rohitg00/2067ab416f7bbe447c1977edaaa681e2)、[WenHao Yu 實測](https://yu-wenhao.com/zh-TW/blog/karpathy-zettelkasten-comparison/))*

---

# 二：架構融合（The Inverted Pipeline）

---

## 💬 先問你一個問題

> **你進入一個完全陌生的研究領域，第一步是什麼？**

**(A)** 找一篇看起來重要的論文，從第一頁開始精讀

**(B)** 先找綜述或全局地圖，了解整體格局，再決定讀哪些論文

---

ACT 假設你選 **(A)**：從單篇出發，原子累積，步步為營。

LLM-Wiki 讓 **(B)** 成為可行的起點：先有全局，再深潛。

> **真正的問題是**：
> 選 (B) 之後，如何確保最終建立的知識仍有原子化的可溯源連結，
> 而不只是「我大概知道這個領域」？

---

## 🆚 兩種架構優劣對比

| 面向       | 傳統 ACT（A 路線） | LLM-Wiki（B 路線） |
| -------- | ------------ | -------------- |
| 起點       | 單篇文獻         | 跨文獻全局          |
| 前期成本     | 高（需精讀才能啟動）   | 低（AI 快速建立地圖）   |
| 原子化連結    | 強（段落級溯源）     | 弱（頁面級聚合）       |
| 跨文獻對話    | 弱（需逐步累積）     | 強（立即可查詢）       |
| 知識所有權    | 高（人類理解驅動）    | 中（AI 編譯，需驗證）   |
| Top-Down | 低（缺乏全局起點）    | 高（天然起點）        |

**融合目標**：用 LLM-Wiki 啟動 Top-Down，用 ACT 的Bottom-up建立知識基礎。

---

## 🔄 反轉流程（Inverted Pipeline）

```
傳統 ACT（A 路線，Bottom-Up）：
單篇 PDF ──► Annotation ──► Connection ──► Thought

反轉流程（融合，TCA-then-ACT）：

NotebookLM（N 篇）
  [Cloud Raw Layer]
        │
        ▼
  全局 Thought                  ← TCA 起點：NLM 生成
   （Briefing Doc + 心智圖）
        │
        ▼
  選定文獻 Deep Dive             ← TCA 中段：人類決策
        │
        ▼
  Annotation Cards（本地）       ← ACT 接手：嚴謹對話
        │
        ▼
  Gear → Connection → Thought   ← ACT 完整流程
```

---

## ☁️ Cloud Layer：NotebookLM 作為 Raw Layer

**定位**：雲端原始文獻倉庫 + 跨文獻 AI 對話介面

**輸入**：30+ 篇 PDF 文獻（範例：[Ilya30 notebook](https://notebooklm.google.com/notebook/64e26507-f5e7-45ba-8be4-ce04b2cd1365)，33 篇基礎 AI 論文）

**主要功能**：

| NLM 功能 | 輸出 | ACT 對應 |
|----------|------|---------|
| `notebook_query` | 跨文獻問答 + 來源引用 | `/connection-query`（但跨 NLM 來源）|
| `studio_create (report)` | Briefing Doc | 轉換為 Thought Note 草稿 |
| `studio_create (mind_map)` | 概念關係圖 | 轉換為 Mermaid，嵌入 Vault |
| `studio_create (data_table)` | 結構化概念清單 | 轉換為 Annotation 卡片 |

---

## 💻 Deep Dive Layer：Local Vault 作為落地區

**定位**：選定文獻的原子化深潛與知識建構

**輸入**：NLM 萃取的原子概念

**落地位置**：`ACT/0️⃣Annotation/{citekey}/cards/`

**流程**：
1. NLM Query → 取得 20-30 個結構化原子概念
2. 格式化為 ACT 卡片（`{citekey}-XXX.md`）
3. 建立主索引 `{citekey}.md`（含 Mermaid 概念圖）

**NLM 是原料，Obsidian是精煉廠。**

---

## 🤖 Assembly Layer：本地 Skills 無縫接手

NLM 卡片進入 Vault 後，啟動 ACT 筆記流：

```
NLM cards
    │
    ▼
/annotation-card-review ──► 敘事草稿
    │
    ▼
/annotation-gear-coaching ──► Connection Gear（英文）
    │
    ▼
/connection-gear-aggregate ──► Connection Notes
    │
    ▼
/thought-refine ──► Thought Notes
```

**NLM 在後期的補充角色**：
- Phase 3 深度對話中補問跨文獻張力
- `/thought-question-challenge` 讓 NLM 提供反例

---

## 📋 層級對應表（LLM-Wiki ↔ ACT Vault）

| LLM-Wiki 層            | ACT Vault 位置        | NotebookLM 角色        |
| --------------------- | ------------------- | -------------------- |
| `raw/`                | NotebookLM Notebook | 雲端原始文獻倉庫             |
| `wiki/`               | `ACT/1️⃣Conn/`      | 生成 Connection 草稿候選   |
| `schema`              | `.claude/skills/`   | NLM 函式補充 ACT Skills  |
| `index.md` + `log.md` | `ACT/ACT space.md`  | `studio_status` 追蹤產出 |

> **無需建立 `raw/` 目錄**：NotebookLM 本身就是 raw layer，不需要複製一份到本地。

---

# 模組三：系統設定與實作

---

## 📥 核心套件

| 套件                         | 說明                       | 必要性 |
| -------------------------- | ------------------------ | --- |
| **Obsidian**               | Vault 主介面                | 必要  |
| → `quickadd`               | 快速新增筆記模板                 | 建議  |
| → `templater-obsidian`     | 進階模板語法                   | 建議  |
| → `dataview`               | 動態查詢 Vault 數據            | 建議  |
| → `lean-obsidian-terminal` | Obsidian 內執行 Claude Code | 選用  |
| google Antigravity         | 執行ACT Skills (額度內免費)     | 必要  |
| **Claude Code CLI**        | 執行 ACT Skills（付費）        | 選用  |
| **NotebookLM MCP**         | 連接 NLM 至 Claude Code CLI | 必要  |

> 📦 示範套件下載：[github.com/SCgeeker/ACT_base/tree/LLM-wiki-exp](https://github.com/SCgeeker/ACT_base/tree/LLM-wiki-exp)

---

## 📂 Vault 結構建議

```
ACT_Base/
├── ACT/
│   ├── ACT space.md          ← 中央儀表板（知識累積狀態）
│   ├── 0️⃣Annotation/        ← NLM 卡片落地區
│   │   └── {citekey}/
│   │       ├── {citekey}.md  ← 主索引（含 Mermaid 圖）
│   │       └── cards/        ← 原子卡片（{citekey}-XXX.md）
│   ├── 1️⃣Conn/              ← Connection Notes
│   └── 2️⃣Thought/           ← Thought Notes
├── Atlas/Sources/            ← LLM-Wiki 參考文獻（8 篇）
├── Templates/                ← 各層 Obsidian 模板
└── .claude/skills/           ← 12 個 Skill 定義
```

---

## 🛠️ Skills 分層一覽

**Annotation 層**（文獻落地）
- `/annotation-card-review <citekey>`：卡片 → 敘事草稿
- `/annotation-gear-coaching <citekey>`：4 階段人機提煉 Gear
- `/annotation-cross-link <citekey>`：識別跨文獻連結
- `/annotation-monitor`：Vault Lint，掃描完成度與孤兒卡片

**Connection 層**（跨文獻合成）
- `/connection-gear-aggregate`：聚合 3+ Gears → Connection 策略
- `/connection-framework-synthesize`：理論框架比較表（≥3 維度）
- `/connection-tension-resolve`：識別並調和理論矛盾

**Thought 層**（原創主張）
- `/thought-refine <title> --focus full`：改善寫作，保留 100% 人類聲音
- `/thought-provenance-audit <title>`：追蹤所有主張至段落級來源
- `/thought-question-assess <title>`：評估晉升為正式可測假說

---

# 四：流程示範

實戰 4 個階段，以 **"Understanding LSTM Networks"** by Christopher Olah 為例

---

## 🟢 Phase 1：跨文獻視野（Cloud Overview）

**目標**：用 NLM 對 33 篇論文取得主題地圖，產出可用的全局 Thought

**操作**：
```
notebook_query →
  "33 篇論文中有哪些跨文獻主題群組？列出 5-7 個主題及對應論文"

studio_create (report)  → Briefing Doc
studio_create (mind_map) → 概念關係圖 → 轉換為 Mermaid
```

本地 AI 將 Briefing Doc 轉換為 Thought Note，嵌入 Mermaid 心智圖。

> 📂 **展示成品**：[[🤔Ilya30 Cross-Paper Synthesis]]

---

## 🔵 Phase 2：單篇深潛（NLM → ACT Cards）

**目標**：選定一篇論文，從 NLM 萃取原子卡片，落地到 Vault

**操作（"Understanding LSTM Networks" 為例）**：
```
notebook_query →
  "從 "Understanding LSTM Networks" 提取 20-30 個原子概念
   格式：ID / 繁體中文標題 / 核心引述 / 相關概念
   語言：繁體中文、台灣學術慣用語"
```

**產出**：n 張 Zettel 卡片 + 主索引 ` Olah-YYYY-XXX.md` + Mermaid 概念圖

> 📂 **展示成品**：[[Karpathy-2015-RNN]]

---

## 🟣 Phase 3：深度對話（Human × AI Coaching）

**目標**：將卡片提煉為具學術價值的 Connection Gear

**操作**：
```
/annotation-gear-coaching Karphaty-2015-Rnn
```

**4 個階段**：
- **Phase 1（AI）**：掃描卡片 → 提出 5-7 個候選洞見，標記關鍵卡片 🔑
- **Phase 2（人類）**：挑選 3-5 個洞見，標記與自身研究的相關性
- **Phase 3（對話）**：AI 針對性追問（如：「這與你的既有研究有何張力？」）
- **Phase 4（組裝）**：人類起草 Gear，AI 審核完整性與句式規範

> 補充：Phase 3 中可對 NLM 補問跨文獻反例或支持證據

---

## 🟠 Phase 4：Gear 組裝（成品輸出）

**目標**：輸出符合學術規範的英文 Connection Gears

**Gear Sentence Style（嚴格執行）**：

| ❌ 禁止 | ✅ 替代 |
|--------|--------|
| 破折號連接子句 | 句號切斷，或明確連接詞 |
| 括號行內列舉 | "including X, Y, and Z" |
| 關係子句（which/that）| 拆成獨立句子 |
| 從屬子句開頭 | 直接 SVO 句型 |

> 📂 **展示成品**：[[Karpathy-2015-RNN]]（Gear Coaching Notes + Final Connection Gears）

> 📊 **兩種工作流比較**：[[Framework_comparison]]
> NLM 版：18 卡片、Gear 完成、概念圖精簡
> 手動版：30 卡片、Gear 區塊空白、Mermaid 圖超過 550 行

---

## 🏁 結語

**反轉流程解決了什麼？**

| 問題          | 傳統 ACT     | 融合方案                     |
| ----------- | ---------- | ------------------------ |
| 進入新領域       | 需先精讀一篇     | LLM-wiki 先給全局地圖          |
| TCA 的罩門     | 無法驗證主張來源   | ACT Skills 強制溯源          |
| LLM-Wiki 孤立 | 無原子化連結深度   | Gear 提供原子連結              |
| LLM-Wiki 孤兒 | 知識不沉澱為個人主張 | Connection Note 顯化個人知識網路 |

**可以從哪裡開始？**
1. 建立你的研究領域 NotebookLM（20-30 篇核心文獻）
2. 跑一次 Phase 1：看看 NLM 給你什麼地圖
3. 選一篇你最想深入的，跑 Phase 2-4

> 📦 所有資源：[github.com/SCgeeker/ACT_base/tree/LLM-wiki-exp](https://github.com/SCgeeker/ACT_base/tree/LLM-wiki-exp)

---

# Q & A

**歡迎討論：**

- 你的研究領域目前如何管理文獻？
- ACT 的哪個 Phase 對你最有吸引力？
- NLM 的哪個功能你最想嘗試？
