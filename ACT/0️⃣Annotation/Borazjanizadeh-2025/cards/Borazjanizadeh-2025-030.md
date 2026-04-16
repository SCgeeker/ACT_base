---
title: "訓練日程：<EOS>詞元權重下調"
summary: |-
  "In TG, end-of-sentence markers (<EOS>) are more frequent than lexical tokens, as they appear at the end of every sentence and are often comparatively easy to predict (strongly signaled by punctuation and syntax). To mitigate this frequency and easy-label imbalance, we apply a frequency-aware reweighting of the token-level loss that down-weights <EOS> targets after an initial warm-up epoch (weight 1.0 for epoch 1, then 0.05 thereafter)[61,62]."
---

## 說明
在ThoughtGestalt (TG) 模型中，句子結束標記（<EOS>）比普通詞彙詞元出現頻率更高，因為它們在每個句子的結尾都會出現，並且通常相對容易預測（由標點符號和語法強烈指示）。為了解決這種頻率高和易於預測標籤之間的不平衡問題，TG模型在訓練中採用了一種頻率感知的詞元級損失重新加權策略。

具體來說，在初始的一個預熱週期（epoch）之後，<EOS>目標詞元的權重會被下調（第一個epoch權重為1.0，之後權重為0.05）。這種權重下調旨在減少模型對預測易於預測的<EOS>詞元的過度關注，從而將更多學習資源導向預測更具挑戰性的詞彙詞元，進一步優化模型的整體性能。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-023]]



**相關** ↔ [[Borazjanizadeh-2025-029]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.3 Training schedules)
- 🎯 **情境**: 描述了TG模型訓練過程中的一個優化細節，用以處理特殊詞元頻率不平衡帶來的挑戰，確保模型能更有效地學習詞彙詞元的預測。

## 個人筆記


🤖 **AI**: <EOS>詞元權重下調的策略是一個實用的工程技巧，用於處理訓練數據中的類別不平衡問題。它確保了模型不會因為過於專注於容易預測的頻繁詞元而忽視了對其他詞彙詞元的學習，這對於提高 [[Borazjanizadeh-2025-009]] 中報告的整體困惑度性能至關重要。
✍️ **Human**:



## 待解問題
除了簡單的權重下調，是否還有其他更複雜的損失加權策略，能夠更好地平衡特殊詞元和詞彙詞元的學習？這種權重調整對模型的長距離理解和生成質量有何影響？
