---
title: "RNN的核心API與`step`函數"
summary: |-
  "At the core, RNNs have a deceptively simple API: They accept an input vector x and give you an output vector y. However, crucially this output vector’s contents are influenced not only by the input you just fed in, but also on the entire history of inputs you’ve fed in in the past. Written as a class, the RNN’s API consists of a single step function: `y = rnn.step(x)`"
---

## 說明
循環神經網路（RNNs）的核心運作機制體現於其簡潔的API（應用程式介面），特別是單一的 `step` 函數。每次調用 `step(x)` 時，RNN不僅基於當前輸入向量 `x` 產生輸出向量 `y`，更重要的是，`y` 的內容還受到過去所有輸入歷史的影響。
這暗示了RNN內部維護著一個持續更新的狀態，使其能夠捕捉序列中的長期依賴關係。`step` 函數是RNN動態行為和記憶能力的具體實現。
此概念屬於「理解」和「應用」層次，解釋了RNN的基本操作。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-004]], [[karpathy_github_io_2015_05_21_rnn-effect-008]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-010]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-006]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: RNN computation
- 🎯 **情境**: 作者在解釋RNNs如何具體運作時，介紹了其核心的 `step` 函數，這是理解RNNs狀態更新和序列處理的基礎。

## 個人筆記


🤖 **AI**: `step` 函數的簡潔性掩蓋了其內部更新的複雜性，特別是在處理長期依賴時。它如何有效地「記住」整個歷史，而不是簡單地疊加？這正是 [[karpathy_github_io_2015_05_21_rnn-effect-014]] 中LSTM等更複雜單元設計的關鍵原因。

✍️ **Human**:



## 待解問題
儘管 `step` 函數概念簡單，但在不同RNNs變體中，其內部實現有何本質區別？這種設計如何影響其記憶容量和處理長序列的能力？
