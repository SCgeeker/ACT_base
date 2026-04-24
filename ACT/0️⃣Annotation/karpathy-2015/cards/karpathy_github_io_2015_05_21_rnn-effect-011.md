---
title: "Vanilla RNN的模型參數"
summary: |-
  "This RNN’s parameters are the three matrices W_hh, W_xh, W_hy."
---

## 說明
Vanilla RNN（香草循環神經網路）的核心參數由三個權重矩陣構成：`W_hh`、`W_xh` 和 `W_hy`。
*   `W_hh`: 連接上一個時間步的隱藏狀態與當前隱藏狀態的權重矩陣。
*   `W_xh`: 連接當前輸入與當前隱藏狀態的權重矩陣。
*   `W_hy`: 連接當前隱藏狀態與輸出向量的權重矩陣。
這些矩陣的初始值通常是隨機設定的，而訓練過程的重點就是調整這些參數，使其能夠產生預期的輸出行為。
此概念屬於「理解」層次，明確了RNN模型可學習的部分。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-010]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-012]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-019]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: RNN computation
- 🎯 **情境**: 在描述Vanilla RNN的 `step` 函數實現後，作者清晰地指出了構成該模型可學習部分的權重矩陣，這是理解RNN訓練目標的基礎。

## 個人筆記


🤖 **AI**: 這三個權重矩陣定義了Vanilla RNN的容量和學習潛力。模型參數的數量和複雜性直接影響訓練的難度和過擬合的風險。這也使得像 [[karpathy_github_io_2015_05_21_rnn-effect-014]] 這樣的LSTM模型，儘管有更多參數，但因其門控機制而能更好地管理信息流和梯度。

✍️ **Human**:



## 待解問題
這些權重矩陣的維度是如何確定的？它們的初始化方法對訓練效果有何影響？
