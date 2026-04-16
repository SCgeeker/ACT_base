---
title: "中間層提取句子表徵的魯棒性"
summary: |-
  "Extracting sentence representations from the last layer, removing context seeding, disabling EOS down-weighting, disabling the stream-length curriculum, and halving the maximum sentence length all increase test perplexity by 0.4–0.7 PPL (about 1–2.4%) relative to baseline."
---

## 說明
在對ThoughtGestalt (TG) 模型進行的消融實驗中，研究還評估了其他設計選擇的影響。這些包括：將句子表徵從最後一層提取（而非默認的中間層）、移除上下文種子、禁用<EOS>詞元權重下調、禁用句子流長度課程學習，以及將最大句子長度減半。

這些改變雖然不像梯度流截斷那樣產生戲劇性的性能下降，但都導致測試困惑度相對基準模型增加了0.4–0.7 PPL（約1–2.4%）。這表明這些設計選擇，儘管看起來是次要的細節，但對於TG模型的整體性能和效率都產生了系統性的積極影響。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-025]], [[Borazjanizadeh-2025-028]], [[Borazjanizadeh-2025-029]], [[Borazjanizadeh-2025-030]]





## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (4.4 Ablations)
- 🎯 **情境**: 作為消融實驗的補充發現，揭示了TG模型中多個看似次要的設計決策共同協作，以實現最佳性能。

## 個人筆記


🤖 **AI**: 這組消融實驗的結果強調了模型設計中「小細節」的重要性。儘管每個單獨的改變可能只導致微小的性能下降，但它們共同構成了一個穩健且優化的系統。這也印證了 [[Borazjanizadeh-2025-025]] 中從中間層提取句子表徵的合理性，以及 [[Borazjanizadeh-2025-028]] 和 [[Borazjanizadeh-2025-030]] 等訓練策略的有效性。
✍️ **Human**:



## 待解問題
這些「小細節」的綜合影響是否存在非線性的互動？如何系統性地分析多個設計選擇之間的協同作用和潛在衝突？
