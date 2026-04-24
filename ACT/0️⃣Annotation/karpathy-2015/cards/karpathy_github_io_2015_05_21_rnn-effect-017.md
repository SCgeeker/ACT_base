---
title: "RNN輸出向量作為下一個字符置信度"
summary: |-
  "We will then observe a sequence of 4-dimensional output vectors (one dimension per character), which we interpret as the confidence the RNN currently assigns to each character coming next in the sequence."
---

## 說明
在字符級語言模型中，循環神經網路（RNN）的輸出是一個向量，其維度與詞彙表的大小相同（例如，詞彙表有4個字符，則輸出是4維向量）。這個輸出向量的每個元素代表了RNN對下一個序列中各個字符可能性的置信度（confidence）。
例如，如果輸出向量的某一維度值很高，就表示RNN認為對應的字符很有可能在當前序列後出現。這些置信度隨後會透過Softmax分類器轉換為概率分佈。
此概念屬於「理解」和「分析」層次，解釋了RNN輸出的含義。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-016]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-018]], [[karpathy_github_io_2015_05_21_rnn-effect-021]]




## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Character-Level Language Models
- 🎯 **情境**: 作者在說明字符級語言模型的運作方式時，解釋了RNN的直接輸出如何被解釋為對下一個字符出現概率的置信度，這是模型做出預測的基礎。

## 個人筆記


🤖 **AI**: 將輸出向量解釋為「置信度」是直觀的，但其數值範圍通常不受限，需要通過Softmax函數（如 [[karpathy_github_io_2015_05_21_rnn-effect-018]] 所述）才能轉化為有效的概率分佈。這種設計允許模型在訓練過程中靈活地調整對不同字符的偏好。

✍️ **Human**:



## 待解問題
在訓練初期，這些置信度是如何分佈的？它們如何隨著訓練進程的推進而演變，最終收斂到一個有意義的預測？
