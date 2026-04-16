---
title: "傳統學習句子表徵的方法 (輔助目標)"
summary: |-
  "Many models learn explicit sentence embeddings by adding extra training objectives on top of language modeling. BERT, for example, adds a Next Sentence Prediction (NSP) loss, where a classifier must decide whether a second sentence truly follow the first or is just a randomly sampled sentence."
---

## 說明
許多現有的語言模型為了學習句子表徵（或句子嵌入），通常會在基本的語言建模目標之上，額外增加一些輔助訓練目標。例如，BERT模型引入了「下一句子預測」（Next Sentence Prediction, NSP）損失，模型需要判斷給定的第二個句子是否是語料庫中緊接第一個句子的真實句子，或是隨機採樣的句子。

此外，還有如SimCSE等對比學習方法，透過將相同句子的不同視圖拉近，並推開不相關句子的嵌入來學習句子表徵。然而，研究表明這些輔助目標有時可能表現脆弱，如果未經仔細調整，甚至可能損害下游任務的泛化能力。

## 連結網絡




**相關** ↔ [[Borazjanizadeh-2025-014]]


**對比** ⚡ [[Borazjanizadeh-2025-008]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works
- 🎯 **情境**: 在比較其他相關工作時，作為傳統學習句子表徵的主要方法之一被提及，突顯了其與TG模型獨特單一目標函數訓練策略的對比。

## 個人筆記


🤖 **AI**: 引入輔助目標來學習句子表徵雖然直觀，但其「脆弱性」和潛在的「損害泛化能力」問題確實是一個痛點。這也正是 [[Borazjanizadeh-2025-008]] 中TG模型採用單一目標函數設計的動機。設計一個既能學習豐富表徵又不會引入額外風險的目標函數，是語言模型研究的永恆挑戰。
✍️ **Human**:



## 待解問題
除了「下一句子預測」和「對比學習」，是否存在其他更穩健、更有效的輔助目標來學習句子表徵？如何理論性地解釋這些輔助目標的脆弱性？
