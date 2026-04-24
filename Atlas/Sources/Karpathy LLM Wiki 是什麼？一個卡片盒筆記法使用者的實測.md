---
title: Karpathy LLM Wiki 是什麼？一個卡片盒筆記法使用者的實測
source: https://yu-wenhao.com/zh-TW/blog/karpathy-zettelkasten-comparison/?fbclid=Iwb21leARFlbRjbGNrBEWVs2V4dG4DYWVtAjExAHNydGMGYXBwX2lkDDM1MDY4NTUzMTcyOAABHk9-9Rh4RTZt-bKQK9Dlw-XxoR8IQPTuvg3_M_q5DLBDSUN_NpORBRS5htoS_aem_s1DWjNmAgJLg_YArQSm-kA
author:
  - "[[WenHao Yu]]"
published: 2026-04-10
created: 2026-04-10
description: 連結已存的Karpathy 推文及增補gist
tags:
  - theme/pkm
  - pkm/methods/llm
---
> Karpathy 的 LLM Wiki pattern 被 AI 圈洗版。身為 Obsidian + LYT 的知識管理使用者，我用他的方法研究他的方法 —— 跑完發現真正的分歧是分類決策：folder、tag、wiki page，三個容器問題形狀一模一樣。

這一週，AI 社群被一篇技術筆記洗版。

作者是 Andrej Karpathy。

如果你沒聽過他 —— 他是 OpenAI 最早的創辦成員之一，後來去 Tesla 當 AI 總監，現在自己開了 Eureka Labs 做 AI 教育。在 AI 圈子裡，他說什麼、隔天就會有一堆人跟著試。

4 月 3 日他[[LLM Knowledge Bases|在 X 發了一段話]]，隔天把整套做法寫成一份[[llm-wiki|Github gist]] 放出來。一週之內 Hacker News、X、Substack 全在討論。

最被瘋狂轉的一句是這個：

> Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase. — Karpathy gist

老實說，這篇紅起來的時候我有點困惑。

這半年 Obsidian + Claude Code / Codex 的組合已經是 PKM 圈的顯學之一。我自己去年底 [從 Roam 轉到 Obsidian](https://yu-wenhao.com/zh-TW/blog/roam-research-to-obsidian/) ，跑 Nick Milo 的 [LYT 框架](https://yu-wenhao.com/zh-TW/blog/lyt-framework-guide/) 加 [Claude Code](https://yu-wenhao.com/zh-TW/blog/claude-code-tutorial/) 當後台，也快半年了。身邊還有幾個朋友在做類似的事。

所以 Karpathy 這篇對我來說，第一眼看過去幾乎沒有新東西。

為什麼這篇會爆成這樣？

帶著這個困惑，我花了半天用他的方法研究他的方法 —— 把 7 份素材丟進去跑了一次 ingest，然後跟我自己用了半年的 LYT 系統做對照。

跑完之後我想跟你說兩件事。

第一，骨架一樣。差在 workflow。

第二，根本的分歧不在技術，在哲學 —— 一張卡到底是什麼？

## Karpathy 說了什麼？

他的核心主張很簡單： **不要做 RAG，改做 wiki** 。

RAG 的做法是每次查詢時才臨時從 raw 文件找答案。Karpathy 的做法是：讓 LLM 作為 compiler，把 raw 文件增量編譯成一份持久化的 markdown wiki，然後一直維護它。

這兩者的根本差異是時間維度：

- **RAG** ：每次查詢 = 重新找答案（stateless、transient）
- **LLM Wiki** ：一次編譯、持續維護（stateful、compounding）

「the wiki is a persistent, compounding artifact. The cross-references are already there. The contradictions have already been flagged.」（wiki 是一個持久的、會累積的產物。交叉引用已經建好了，矛盾已經被標出來了。）

Karpathy 的理由是這個：

> The tedious part of maintaining a knowledge base is not the reading or the thinking — it’s the bookkeeping. Humans abandon wikis because the maintenance burden grows faster than the value. LLMs don’t get bored. — Karpathy gist

人會放棄 wiki，因為維護成本超過回報。LLM 不會累、不會忘記更新 cross-reference、可以一次動 15 個檔案 —— 維護成本被壓到接近零。

所以這個 pattern 的核心不是「讓 AI 寫筆記」。是「把 bookkeeping 壓到接近零，人才有力氣思考」。

順帶一提，Karpathy 把這個 pattern 連回 Vannevar Bush 1945 的 Memex 願景。Bush 80 年前就想做「人的延伸記憶系統」，但他解決不了一件事 —— 誰來維護？Karpathy 對這句話的回答是：

> The part he couldn’t solve was who does the maintenance. The LLM handles that.

這個歷史縱深讓這個 pattern 不只是 2026 年的一時熱潮。是一個 80 年前的願景終於有了答案。

## 骨架相同，但長大方式不同

我打開自己在 Obsidian 上的知識管理系統對照 Karpathy 的 gist，骨架幾乎一樣：

| Karpathy Pattern | 我的 LYT |
| --- | --- |
| `raw/` （原始來源） | `Atlas/Sources/` |
| `wiki/` （LLM 維護的知識頁） | `Atlas/Dots/` + `Maps/` |
| schema 檔（規則設定） | `CLAUDE.md` + 各 `SKILL.md` |
| `index.md` （索引） | `Maps/` MOC |

Karpathy 的 gist 是工具不可知的 —— 他同時列了 Claude Code、OpenAI Codex、OpenCode 等選項。我用 Claude Code，所以對照我這邊用 `CLAUDE.md` 。

四個層對到了。但骨架像不代表兩條路一樣 —— 我用 LYT 半年，搭配 Claude Code 打了一套 [完整的 AI 工作流](https://yu-wenhao.com/zh-TW/blog/personal-panopticon/) ，知識庫一直在長大，只是長大的方式跟 Karpathy 描述的完全不同。

## 我從 Karpathy 學到了什麼？

跑完骨架對照之後，我發現 Karpathy 的 pattern 有幾件事是我的系統還沒做到的。

**Ingest 時的矛盾偵測** 。新 source 進來，LLM 會比對新資訊跟舊 wiki page 的衝突，標出矛盾，留給人判斷。我的原子卡片目前不會互相比對。

**跨 page 連鎖更新** 。一個新 source 可能同時更新 10-15 張 wiki page。我建新卡時會補連結，但不會動舊卡的內文。

**Lint** 。定期掃整座 wiki 做健康檢查 —— 找矛盾、找孤立 page、找過期內容。更厲害的是它會偵測概念缺口：「你在好幾個地方提到這個概念，但沒有獨立的 page」—— LLM 主動建議你建一張。

這些功能技術上都能加進我的系統。但 Karpathy 的貢獻是 **他先把這些想清楚了，然後寫成一份任何人都能用的 pattern** 。

學到了這些之後，剩下一個繞不過去的問題。

## 一張卡到底是什麼？

LYT 的答案是一個 **原子概念** 。一張卡一件事，邊界由概念本身決定。好處是歸檔不用想太多，新東西進來就開新卡。代價是你要掌握一個主題的最新狀態，得靠 MOC 和連結自己拼圖。

Karpathy 的答案是一個 **主題聚合** 。一張 wiki page 是那個主題目前的 best-of 總整理。10 個 sources 可能被 LLM 併進 1-2 張 page。好處是打開一張就看到全貌，不用自己拼。

但我昨天跑 ingest 的時候就卡住了 —— **主題的邊界在哪？** 幾份 source 該併成一張 page、哪些該獨立出來？最後跑出來的數量和邊界，都是我臨時決定的，不是某個規則告訴我的。

然後我意識到：這個問題我見過。Evernote 時代你在問「這個筆記放哪個 folder」。Notion 早期你在問「這個頁面打哪些 tag」。Karpathy wiki 現在在問「這個 source 併進哪張 wiki page」。

三個問題的形狀一模一樣： **對一個新進來的東西，你要決定它屬於哪個容器** 。

卡片盒筆記法的核心概念 —— 原子化 —— 就是在繞開這個問題。一張卡一個概念，連結取代分類。新東西進來，同一個概念就補在舊卡上、不同概念就開新卡。邊界由概念本身決定，不用想「歸到哪個容器」。我用的 [LYT](https://yu-wenhao.com/zh-TW/blog/lyt-framework-guide/) 繼承了這個核心，加上 MOC 和 AI 整合 —— 不是 pure Zettelkasten，但原子化的精神是一樣的。

Karpathy 的主題聚合是往回走。它用 LLM 的能力把 compound 成本壓低，但沒解決「容器邊界在哪」這個老問題。

## 反對的聲音

容器邊界是我自己跑完實驗後的觀察。但 HN 上還有兩層不同角度的反對，攻擊的都是 **人類的懶惰** ，不是 LLM 的能力。

### 反對一：Model Collapse（技術面）

除了容器邊界問題，Karpathy 的 pattern 還有一個更根本的技術擔憂。HN 上有人直接點名：

> I don’t see why this wouldn’t just lead to model collapse. The compounding will just be rewriting valid information with less sense information.

論點是：LLM 寫出來的 wiki 本身就有資訊損耗 —— 看起來通順但細節被磨平、風格被單一化。下次 ingest 時 LLM 會讀到舊 wiki + 新 source，等於「LLM 在自己寫的東西上再寫」。長期下來可能變成平均的平均的平均，細節慢慢消失。這個現象 AI 圈有個名字叫 **Model Collapse** ， [2024 年 Nature 的論文](https://www.nature.com/articles/s41586-024-07566-x) 有完整論證。

HN thread 上有反駁的聲音，但那些反駁針對的是 LLM 訓練場景，跟 Karpathy 的 ingest 場景不完全一樣。這個 pattern 會不會真的觸發 Model Collapse，目前還沒人跑夠久可以證明。

### 反對二：Vibe Thinking（認知面）

這個反對最狠。HN 原文：

> Rule of thumb: if you find yourself having to come up with instead of what it helps you produce, ask yourself ‘am I thinking?’

有深度的寫作是從 **produce** （生產）的過程中 **come up with** （想出）東西。如果你只是讓 AI produce、你只負責 come up with 問題，那你可能根本沒在思考。

Karpathy 其實在 gist 裡有預先反駁這點：

> The human’s job is to curate sources, direct the analysis, ask good questions, and think about what it all means.

「think about what it all means」這句話是他留給人類的。但 HN 的論點是： **這是理論上的分工，實際上很少人會做到** 。

「vibe coding」是一個已經存在的現象 —— 不懂原理就讓 AI 寫 code，結果能跑但你不懂。HN 擔心的是 vibe thinking —— 把「整理」外包等於把「思考」外包，wiki 看起來很有組織但你根本沒內化。

### 那對我來說真正的問題是什麼？

這兩個反對聲音都在攻擊人類的懶惰。但對我來說，它們不是真正的問題。

我也懶。但我的防禦是前置的 —— 新東西進來先跟 LLM 討論到我理解，理解完才決定要不要歸檔。思考在對話裡發生，歸檔是思考完的結果。所以進知識庫的每張卡都是我驗證過的，LLM 下次讀到的不是它自己 compound 出來的東西，Model Collapse 的前提就不成立。Vibe Thinking 也一樣，歸檔是理解完的儲存，不是理解前的外包。

而前面提到的矛盾偵測、lint、跨卡改寫，我也都準備整合進自己的系統。

真正讓我不搬家的原因只有一個： **容器** 。

兩條路都用 LLM 做 compound，bookkeeping 成本兩邊都壓得下來。但 Karpathy 的 wiki page 是主題聚合 —— 你要決定主題邊界在哪、哪些東西該併進同一張 page。LYT 的原子卡片繞開了這個問題 —— 一張卡一個概念，不用想歸到哪裡。

如果你有一個明確的主題要長期維護，而且對「這個東西該放哪張 page」這類決策不覺得煩，Karpathy 的 pattern 值得試。去讀他的 [gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) ，搭配 Mehmet 的 [實作文章](https://mehmetgoekce.substack.com/p/i-built-karpathys-llm-wiki-with-claude) 。

如果你跟我一樣，從 folder 出來、從 tag 出來，不想再走進另一個分類系統 —— 那原子化可能更適合你。

我用他的方法研究他的方法，結果沒讓我換系統。但讓我搞清楚一件事：兩條路的分歧不在技術，在你對分類的容忍度。

---

### 延伸閱讀

想看我怎麼把 LYT + Claude Code 串成一套完整的 AI 工作流？ [這篇是完整介紹](https://yu-wenhao.com/zh-TW/blog/personal-panopticon/) ——從每天早上的「開工」到知識庫、郵件、會議、目標管理全部串起來。

*如果這篇讓你有了想法， [訂閱每週一封信](https://yu-wenhao.com/zh-TW/) ——我固定寫 AI 工作流、和一路上想通的事。*

*想聊聊怎麼把 AI 融入你的工作流？ [看看我的服務](https://yu-wenhao.com/zh-TW/services/) 。*


## 常見問題

Karpathy 的 LLM Wiki 跟 RAG 有什麼不同？

RAG 每次查詢重新從 raw 文件找答案，什麼都不留。LLM Wiki 讓 LLM 把 raw 增量編譯成一份持久化的知識管理 wiki，然後一直維護它。差別是時間維度 —— RAG 每次重新推導，wiki 把推導結果存起來持續累積。

什麼是 Model Collapse？

LLM 反覆讀自己寫的東西再改寫，長期下來細節被磨平、風格單一化 —— 平均的平均的平均。Nature 2024 有論文論證。這是 HN 對 Karpathy pattern 最大的技術擔憂。

卡片盒筆記法和 Karpathy LLM Wiki 的核心差別是什麼？

容器。卡片盒筆記法的原子卡片一張一個概念，連結取代分類，不用想「這個東西歸哪裡」。Karpathy 的 wiki page 是主題聚合，一張 page 裝一個主題的所有東西，但你要決定主題邊界在哪。這是 folder 和 tag 時代的老問題換了個皮。

我該用 Karpathy 的方法嗎？

問自己一個問題：你對「這個東西該放哪」這類分類決策煩不煩？如果不煩，而且有明確的主題要長期維護，Karpathy 的 pattern 值得試。如果你跟我一樣，從 folder 出來、從 tag 出來，不想再走進另一個分類系統，那卡片盒筆記法的原子化路線可能更適合你。