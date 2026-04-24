---
title: "訓練循環網路是程式的優化"
summary: |-
  "If training vanilla neural nets is optimization over functions, training recurrent nets is optimization over programs."
---

## 說明
作者提出一個深刻的觀點：如果訓練傳統神經網路（vanilla neural nets）是針對函數（functions）進行優化，那麼訓練循環神經網路（recurrent nets）則是針對程式（programs）進行優化。
這個類比強調了RNNs不僅學習輸入和輸出之間的靜態映射關係，它們還學習如何動態地處理信息，如同一個具有內部狀態和控制流的程式。這改變了我們對「學習」本身的理解，從簡單的映射到複雜的動態系統。
此概念屬於「分析」和「評估」層次，提供了理解RNNs訓練過程的哲學視角。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-006]]




**對比** ⚡ [[karpathy_github_io_2015_05_21_rnn-effect-005]]


## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Recurrent Neural Networks
- 🎯 **情境**: 在闡述RNNs的圖靈完備性和其作為程式的性質後，作者提煉出這一哲學性論斷，以概括RNNs訓練的本質。

## 個人筆記


🤖 **AI**: 將訓練RNNs視為「程式優化」是一個強大的隱喻，它強調了RNNs學習動態行為的能力。然而，這也引出了一個問題：我們如何評估一個「程式」的優化程度，而不僅僅是函數的輸出？這與 [[karpathy_github_io_2015_05_21_rnn-effect-012]] 中提到的「損失函數」在程式優化中的作用息息相關。

✍️ **Human**:



## 待解問題
「程式優化」這個概念如何量化？它是否為設計更有效訓練算法提供了新的視角？
