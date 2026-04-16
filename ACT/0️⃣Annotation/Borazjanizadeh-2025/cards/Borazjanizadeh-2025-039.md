---
title: "Recurrent Memory Transformer (RMT)"
summary: |-
  "Recurrent Memory Transformer adds dedicated memory tokens that are passed between segments and updated by self-attention, providing a differentiable memory channel across long sequences [49]."
---

## 說明
Recurrent Memory Transformer (RMT) 是一種旨在為Transformer模型引入可差異化記憶通道的方法。它透過添加「專用記憶詞元」（dedicated memory tokens）來實現這一目標。這些記憶詞元在文本區段之間傳遞，並透過自注意力機制不斷更新。

RMT的設計為模型處理長序列提供了一個明確的記憶通道，允許信息在區段之間流動並累積。由於這些記憶詞元是可差異化的，因此它們可以透過反向傳播進行優化，從而提高模型學習和利用長期上下文的能力。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-015]]



**相關** ↔ [[Borazjanizadeh-2025-016]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works (Recurrence and memory in Transformers)
- 🎯 **情境**: 在討論Transformer中遞歸與記憶的相關工作時，作為一種引入可差異化記憶詞元以處理長序列的模型被提及，與TG模型在記憶設計上存在異同。

## 個人筆記


🤖 **AI**: RMT的「專用記憶詞元」概念與TG的「句子級要旨」有相似之處，都在於提供一個可差異化的記憶通道。然而，RMT的記憶詞元編碼的是「任意詞元序列」的信息，而 [[Borazjanizadeh-2025-016]] 中TG的記憶詞元則編碼「語義連貫的句子級要旨」。這種語義化的記憶可能使得TG在抽象能力上更具優勢。
✍️ **Human**:



## 待解問題
RMT中的記憶詞元數量如何影響性能和計算成本？是否可以將RMT的記憶詞元設計與TG的句子級要旨相結合，以獲得更強大的記憶能力？
