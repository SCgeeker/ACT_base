---
title: "Memorizing Transformers (外部鍵值存儲)"
summary: |-
  "Memorizing Transformers, on the other hand, add an external key–value store of past activations that can be queried with kNN retrieval at inference time, extending the effective context while keeping the memory non-differentiable [50]."
---

## 說明
Memorizing Transformers 採取了另一種不同的策略來擴展Transformer的上下文能力。它們添加了一個「外部的鍵值存儲」（external key–value store），儲存了過去的激活狀態。在推理時，模型可以透過kNN（k-最近鄰）檢索來查詢這個外部存儲。

這種方法有效地擴展了模型的上下文範圍，使其能夠訪問超出其固定注意力窗口的信息。然而，與ThoughtGestalt (TG) 模型不同的是，這個外部記憶通常是「非差異化的」（non-differentiable）。這意味著它不能透過反向傳播直接進行優化，而是作為一個外部資源在推理時被查詢。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-015]]




**對比** ⚡ [[Borazjanizadeh-2025-016]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works (Recurrence and memory in Transformers)
- 🎯 **情境**: 在討論Transformer中遞歸與記憶的相關工作時，作為一種引入非差異化外部記憶以處理長序列的模型被提及，用於突顯其與TG模型在記憶可差異化上的根本區別。

## 個人筆記


🤖 **AI**: Memorizing Transformers的非差異化記憶方法，雖然擴展了上下文，但其無法透過梯度反向傳播進行優化，這限制了它學習和適應新模式的能力。這與 [[Borazjanizadeh-2025-016]] 中TG模型的可差異化記憶形成了鮮明對比，TG的記憶能夠從訓練中不斷學習和精煉。
✍️ **Human**:



## 待解問題
如何將非差異化記憶的效率和大規模儲存優勢，與可差異化記憶的學習能力相結合？是否存在一種混合記憶系統，能夠同時利用兩者的長處？
