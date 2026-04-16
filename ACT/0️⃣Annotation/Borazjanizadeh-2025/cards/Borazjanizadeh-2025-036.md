---
title: "訓練設置與評估協議"
summary: |-
  "All models are pre-trained on fixed subsets of the WikiText-103 training split, holding the validation and test sets fixed across experiments [64]. All reported losses and perplexities are computed only over lexical tokens: we exclude special-token label positions (e.g., the position predicting frequent end-of-sentence and end-of-document tokens, <EOS> and <EOD> respectively) from both reporting and checkpoint selection."
---

## 說明
本研究中的所有模型都在WikiText-103訓練集的固定子集上進行預訓練，並在所有實驗中保持相同的驗證集和測試集。這確保了模型之間的比較具有一致性。在報告損失和困惑度時，只計算詞彙詞元的結果，排除了特殊詞元（例如<EOS>和<EOD>）的標籤位置。

這種評估協議對於模型選擇和性能報告至關重要。特殊詞元通常頻率高且容易預測，將其排除在外可以更準確地反映模型對實際語言內容的理解和生成能力。優化器採用AdamW，學習率為2.5e-4，並使用餘弦退火和2%的預熱週期，最佳模型透過最低驗證困惑度選取。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-035]]



**相關** ↔ [[Borazjanizadeh-2025-030]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (Experimental setup)
- 🎯 **情境**: 詳細描述了所有實驗的共同設置、數據集選擇、評估標準和訓練超參數，為讀者理解實驗結果的可靠性和有效性提供了必要背景。

## 個人筆記


🤖 **AI**: 評估協議的嚴格性對於科學研究至關重要。排除特殊詞元來計算困惑度，是為了更公平地衡量模型在生成有意義內容方面的能力，這與 [[Borazjanizadeh-2025-030]] 中下調<EOS>權重的訓練策略是相輔相成的。
✍️ **Human**:



## 待解問題
如果將特殊詞元納入困惑度計算，結果會如何變化？在某些需要精確預測特殊詞元的任務中，這種排除策略是否仍適用？
