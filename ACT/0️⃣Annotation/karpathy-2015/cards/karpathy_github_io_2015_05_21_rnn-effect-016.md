---
title: "字符的1-of-k編碼"
summary: |-
  "Concretely, we will encode each character into a vector using 1-of-k encoding (i.e. all zero except for a single one at the index of the character in the vocabulary), and feed them into the RNN one at a time with the step function."
---

## 說明
在字符級語言模型中，每個字符都需要轉換成數值向量才能被循環神經網路（RNN）處理。這裡採用的是1-of-k編碼（又稱獨熱編碼，One-hot encoding），即為詞彙表中的每個字符分配一個唯一的索引。當表示某個字符時，創建一個長度為詞彙表大小的向量，該字符對應索引位置的值設為1，其餘位置均為0。
這些1-of-k編碼的字符向量隨後會一個接一個地透過RNN的 `step` 函數輸入到模型中。
此概念屬於「理解」和「應用」層次，解釋了文本數據輸入RNN前的準備工作。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-015]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-017]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-009]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Character-Level Language Models
- 🎯 **情境**: 作者在闡述字符級語言模型的具體實現細節時，首先介紹了如何將字符轉換為機器可理解的數值形式，這是模型訓練前的基本預處理步驟。

## 個人筆記


🤖 **AI**: 1-of-k 編碼雖然簡單直觀，但它存在維度災難和無法捕捉字符間語義關係的問題。對於大型詞彙表，向量會非常稀疏且維度高。更先進的方法，如字符嵌入（character embeddings），可以學習到字符的稠密表示並捕捉語義相似性。這與 [[karpathy_github_io_2015_05_21_rnn-effect-011]] 討論的模型參數如何學習這些潛在關係有關。

✍️ **Human**:



## 待解問題
除了1-of-k編碼，還有哪些字符編碼方式適用於RNNs？它們各自的優缺點是什麼？
