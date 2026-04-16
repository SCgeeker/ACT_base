---
title: "TG模型擴展性：每層容量增加"
summary: |-
  "Overall, these results show that allocating additional parameter to TG can yield further gains and that adding per-layer cross and self attention is an effective route to scale TG."
---

## 說明
在消融實驗中，研究探索了增加ThoughtGestalt (TG) 模型每層容量對性能的影響。基線TG模型每層交替進行句子內自注意力（Self-attention）和記憶交叉注意力（Cross-attention）。實驗測試了兩種更高容量的變體：串行Self→Cross排序和並行Self&Cross排序。

結果顯示，Self→Cross排序的變體將測試困惑度從29.8降低到29.4，雖然模型參數量從85M增加到114M（+34%），且吞吐量略有下降。並行變體的性能提升較小。這表明，為TG模型分配額外參數可以帶來進一步的性能提升，並且在每層中增加自注意力和交叉注意力是擴展TG模型的有效途徑。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-010]]



**相關** ↔ [[Borazjanizadeh-2025-021]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (4.4 Ablations)
- 🎯 **情境**: 作為消融實驗的一部分，旨在探索TG模型在增加模型容量和複雜度時的性能擴展潛力，證明了其設計能夠從額外參數中獲益。

## 個人筆記


🤖 **AI**: 增加每層容量並非總能帶來性能提升，但TG模型的結果表明，在其獨特的雙層抽象框架下，增加自注意力與交叉注意力的組合能夠有效利用額外參數。這可能因為更強的層內計算能力可以更好地整合 [[Borazjanizadeh-2025-006]] 中的詞元和句子級信息。
✍️ **Human**:



## 待解問題
在增加模型容量的同時，如何避免過擬合並確保性能增益在更廣泛的任務中保持穩定？是否存在一種自動化機制來最佳化每層的注意力結構？
