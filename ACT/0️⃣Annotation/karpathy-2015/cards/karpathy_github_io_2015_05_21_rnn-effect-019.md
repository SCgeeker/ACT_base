---
title: "採用迷你批次隨機梯度下降與自適應學習率方法"
summary: |-
  "The RNN is trained with mini-batch Stochastic Gradient Descent and I like to use RMSProp or Adam (per-parameter adaptive learning rate methods) to stablilize the updates."
---

## 說明
循環神經網路（RNN）的訓練過程採用迷你批次隨機梯度下降（mini-batch Stochastic Gradient Descent, SGD）作為主要的優化算法。SGD是一種迭代優化算法，它透過計算損失函數對於模型參數的梯度，然後沿著負梯度方向更新參數。迷你批次的使用可以在計算效率和收斂穩定性之間取得平衡。
為了進一步穩定訓練更新，作者偏好使用RMSProp或Adam等逐參數自適應學習率方法。這些方法會根據每個參數的歷史梯度信息自動調整其學習率，從而加快收斂速度並提高訓練的穩定性，尤其是在深度網路中。
此概念屬於「應用」和「評估」層次，說明了RNN訓練的實用技巧。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-012]], [[karpathy_github_io_2015_05_21_rnn-effect-018]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-020]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-003]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Character-Level Language Models
- 🎯 **情境**: 在介紹了字符級語言模型的損失函數後，作者進一步說明了實際訓練中所使用的優化方法，強調這些方法對訓練穩定性的重要性。

## 個人筆記


🤖 **AI**: 自適應學習率方法如RMSProp和Adam對於深度學習模型的訓練至關重要，它們能有效緩解梯度不穩定問題，並加快收斂。這也可能是 [[karpathy_github_io_2015_05_21_rnn-effect-003]] 中作者認為RNNs「不難訓練」的原因之一，因為優化技術的進步降低了手動調優的難度。

✍️ **Human**:



## 待解問題
RMSProp和Adam在RNN訓練中表現各有何特點？在不同類型的文本數據集上，哪種優化器更為推薦？
