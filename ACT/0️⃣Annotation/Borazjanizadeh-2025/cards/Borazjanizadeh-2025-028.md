---
title: "上下文種子 (Context Seeding)"
summary: |-
  "In standard Transformers, the prediction of the first token relies on a static <BOS> embedding, lacking local context. Because TG resets the self-attention window at every sentence boundary, this issue is exacerbated. To address this, we replace the static <BOS> embedding for sentences with the preceding sentence representation mt−1: e_t,0 ← m_t−1."
---

## 說明
在標準Transformer模型中，第一個詞元的預測通常僅依賴於一個靜態的<BOS>嵌入，缺乏任何局部語境。對於ThoughtGestalt (TG) 模型來說，由於它會在每個句子邊界重置自注意力窗口，這個問題會被放大。為了彌補這一點，TG引入了「上下文種子」機制。

具體來說，TG將靜態的<BOS>嵌入替換為前一個句子的表徵mt-1。這使得新句子的起始詞元能夠轉化為一個語境化的狀態。因此，新句子的第一個詞彙詞元可以透過兩個互補的途徑訪問先前的上下文：(1) 對記憶的交叉注意力，以及 (2) 對第0個位置的局部自注意力，而這個位置現在顯式地編碼了前一個句子的表徵。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-023]]


**導向** → [[Borazjanizadeh-2025-027]]


**相關** ↔ [[Borazjanizadeh-2025-008]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.2 Model)
- 🎯 **情境**: 描述了TG模型如何解決在新句子開始時缺乏上下文的問題，透過將前一個句子的高層次表徵作為新句子的初始上下文，從而提高模型在新句子開始時的預測能力。

## 個人筆記


🤖 **AI**: 上下文種子是TG模型確保連續語義流動的關鍵機制。它避免了新句子從「白紙」開始，有效地將 [[Borazjanizadeh-2025-005]] 中提到的「思想」狀態從一個句子傳遞到下一個句子。這項設計的成功，說明了上下文的初始化對於序列模型性能的重要性。它也能解釋為何 [[Borazjanizadeh-2025-020]] 中斷梯度流會導致性能大幅下降。
✍️ **Human**:



## 待解問題
除了前一個句子表徵，是否可以將更多先前句子的綜合信息或文檔級信息作為上下文種子，以提供更豐富的初始語境？
