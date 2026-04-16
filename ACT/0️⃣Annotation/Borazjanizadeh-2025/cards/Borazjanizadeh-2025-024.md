---
title: "數據準備：句子流作為訓練範例與批次構建"
summary: |-
  "TG retains the computation graph of sentence representations written to memory to learn sentence encodings via the next-token prediction loss. Although at any sentence step t, the model only attends directly to the most recent M sentence representations (where M is the memory capacity), the computation graph for those stored representations includes their own cross-attention to earlier sentences."
---

## 說明
為了訓練ThoughtGestalt (TG) 模型，文檔會被切分成連續的「句子流」（sentence streams），每個流最多包含S個句子。每個句子流作為一個獨立的訓練範例，並且在處理完一個流後，記憶會被重置。這種策略旨在保持長距離語境化，同時限制反向傳播的最大深度，使訓練在計算上可行。

由於TG模型會保留寫入記憶的句子表徵的計算圖，以便透過下一詞元預測損失來學習句子編碼，梯度依賴鏈會遞歸地延伸。因此，切割句子流限制了計算圖的深度，避免了無界深度反向傳播帶來的計算挑戰。批次構建則透過統一採樣句子流來穩定GPU內存使用和優化。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-023]]


**導向** → [[Borazjanizadeh-2025-025]]


**相關** ↔ [[Borazjanizadeh-2025-029]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.1 Data Preparation)
- 🎯 **情境**: 描述了TG模型如何將預處理好的句子組織成訓練範例，特別強調了句子流切割策略對於管理計算圖深度和確保訓練可追溯性的重要性。

## 個人筆記


🤖 **AI**: 句子流切割是TG模型在實際訓練中平衡性能和效率的關鍵策略。它巧妙地解決了 [[Borazjanizadeh-2025-020]] 中提到的計算圖深度無限增長的問題。然而，這種截斷記憶的方式是否會在某些情況下限制模型對極長距離依賴的學習能力？這可能是一個權衡。
✍️ **Human**:



## 待解問題
句子流的最大長度S如何影響模型的長期依賴學習能力和訓練效率？是否存在動態調整S的策略，以更好地適應不同的文檔長度和數據複雜度？
