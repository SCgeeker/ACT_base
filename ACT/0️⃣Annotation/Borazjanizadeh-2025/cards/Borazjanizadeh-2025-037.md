---
title: "Transformer-XL 的區段級遞歸"
summary: |-
  "Transformer-XL caches hidden states from previous segments and lets the current segment attend to them, providing segment-level recurrence but truncating gradients at the cached states."
---

## 說明
Transformer-XL 是一種將Transformer模型擴展到處理長序列的方法。它透過快取（cache）來自先前區段的隱藏狀態，使得當前區段能夠關注這些被快取的狀態。這種機制提供了「區段級的遞歸」（segment-level recurrence），允許模型整合超越單一固定上下文窗口的信息。

然而，Transformer-XL的一個關鍵特點是，梯度在這些快取的狀態處被截斷。這意味著來自當前區段的損失無法反向傳播回優化先前區段的參數。儘管這種梯度截斷有助於簡化計算，但也可能限制模型在學習長距離依賴和優化早期表徵方面的能力。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-015]]




**對比** ⚡ [[Borazjanizadeh-2025-016]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works (Recurrence and memory in Transformers)
- 🎯 **情境**: 在比較Transformer中遞歸與記憶的相關工作時，作為一種具有代表性的長上下文處理模型被提及，用於突顯其與TG模型在梯度流處理上的差異。

## 個人筆記


🤖 **AI**: Transformer-XL的梯度截斷策略是效率與優化深度之間的權衡。相較於 [[Borazjanizadeh-2025-016]] 中TG模型的可差異化記憶和端到端梯度流，Transformer-XL可能在極長的、需要深層理解的依賴關係上表現出局限性，儘管它在計算上更輕量。
✍️ **Human**:



## 待解問題
在何種情況下，梯度截斷的負面影響可以被接受或最小化？是否存在一種選擇性梯度流動的方法，能夠在性能和效率之間找到更好的平衡點？
