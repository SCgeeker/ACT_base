---
title: "固定詞元跨度遞歸 (Fixed Token-Span Recurrence)"
summary: |-
  "To determine if TG’s performance gains are attributable specifically to using semantically coherent text segments for recurrence/compression, here we evaluate TG with an identical architecture and training procedure, but replace sentence segmentation with fixed token spans of length N ∈ {25, 50, 75} lexical tokens (with N=25 chosen to match the average sentence length in our corpus)."
---

## 說明
這項對照實驗旨在確認ThoughtGestalt (TG) 模型的性能增益是否確實來自於其使用「語義連貫的文本區段」（即句子）進行遞歸和壓縮。實驗中，採用與TG相同的架構和訓練程序，但將句子分割替換為固定長度的詞元跨度（例如25、50、75個詞元），並將每個跨度視為一個「TG句子步驟」。

結果顯示，固定詞元跨度遞歸模型的性能普遍不如基於句子的TG模型。即使增加跨度長度，也未能彌合與TG之間的差距。這項發現強烈支持了TG模型的優勢源於其壓縮語義連貫單元的能力：句子邊界提供了比任意詞元塊更優越的事件分割和記憶組織目標。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-006]]




**對比** ⚡ [[Borazjanizadeh-2025-007]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (4.2 Other Baselines)
- 🎯 **情境**: 作為消融實驗的一部分，用來證明TG模型在性能上的優勢並非僅來自於遞歸或壓縮本身，而是特異性地來自於對語義連貫的句子單元的處理。

## 個人筆記


🤖 **AI**: 固定詞元跨度遞歸的實驗結果，為 [[Borazjanizadeh-2025-005]] 中認知科學關於「整體概念」和「事件分割」的理論提供了強有力的實證支持。這表明，即使採用了相似的遞歸機制，但如果壓縮的單元不具備語義連貫性，模型的性能也會大打折扣。
✍️ **Human**:



## 待解問題
除了句子，是否存在其他自然語言中的語義單元（如子句、話語單元），在作為遞歸和壓縮的單位時，能夠提供比固定詞元跨度更好的性能？
