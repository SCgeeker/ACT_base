---
title: "Block-Recurrent Transformers"
summary: |-
  "Block-Recurrent Transformers apply a Transformer layer recurrently over blocks of tokens, with a recurrent state that each block attends to, combining local self-attention within a block with an RNN-like state that carries information across blocks [48]."
---

## 說明
Block-Recurrent Transformers 是另一種旨在擴展Transformer模型處理長序列能力的方法。它將一個Transformer層遞歸地應用於多個詞元區塊（blocks of tokens）。每個區塊不僅在其內部執行局部自注意力，還會關注一個「循環狀態」（recurrent state）。

這個循環狀態扮演著類似RNN（循環神經網絡）的角色，負責將信息從一個區塊傳遞到下一個區塊。這種設計結合了Transformer在局部上下文處理上的強大能力與RNN在跨區塊信息傳遞上的優勢，從而能夠處理超出單一注意力窗口限制的長距離依賴。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-015]]



**相關** ↔ [[Borazjanizadeh-2025-037]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works (Recurrence and memory in Transformers)
- 🎯 **情境**: 在討論Transformer中遞歸與記憶的相關工作時，作為一種結合局部自注意力和循環狀態以處理長上下文的模型被提及。

## 個人筆記


🤖 **AI**: Block-Recurrent Transformers的設計嘗試融合Transformer和RNN的優勢，以處理長序列。然而，其「RNN-like狀態」的本質可能仍會受到RNN訓練穩定性問題的影響，尤其是在極長序列上。這也突顯了 [[Borazjanizadeh-2025-016]] 中TG模型利用語義化的「句子級要旨」作為循環狀態的優勢，可能提供了更穩健的信息載體。
✍️ **Human**:



## 待解問題
循環狀態的設計對Block-Recurrent Transformers的性能和穩定性有何關鍵影響？如何評估其在不同長度依賴任務上的實際表現？
