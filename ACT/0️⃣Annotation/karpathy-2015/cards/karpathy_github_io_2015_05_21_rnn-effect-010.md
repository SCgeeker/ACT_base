---
title: "Vanilla RNN的隱藏狀態更新機制"
summary: |-
  "Here is an implementation of the step function in a Vanilla RNN: `self.h = np.tanh(np.dot(self.W_hh, self.h) + np.dot(self.W_xh, x))`"
---

## 說明
在最簡單的Vanilla RNN（香草循環神經網路）中，`step` 函數的核心是更新其內部隱藏狀態 `self.h`。這個更新透過兩個主要部分組成：一部分基於前一個時間步的隱藏狀態 `self.h`（乘以權重矩陣 `W_hh`），另一部分基於當前輸入 `x`（乘以權重矩陣 `W_xh`）。兩者相加後，再通過非線性激活函數 `np.tanh` 進行壓縮，形成新的隱藏狀態。
此機制允許RNN將當前輸入與過去信息（由前一隱藏狀態表示）結合起來，形成一個新的、記憶了歷史信息的狀態。
此概念屬於「理解」和「應用」層次，詳細闡釋了RNNs的內部運算。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-009]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-011]], [[karpathy_github_io_2015_05_21_rnn-effect-012]]



**對比** ⚡ [[karpathy_github_io_2015_05_21_rnn-effect-014]]


## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: RNN computation
- 🎯 **情境**: 作者提供了一個Vanilla RNN中 `step` 函數的具體Python/Numpy實現，用以解釋隱藏狀態 `h` 是如何被更新的，這是理解RNNs工作原理的關鍵。

## 個人筆記


🤖 **AI**: Vanilla RNN的隱藏狀態更新機制雖然簡潔，但其簡單的乘加和tanh激活容易導致梯度消失或爆炸問題，尤其是在處理長序列時。這正是 [[karpathy_github_io_2015_05_21_rnn-effect-014]] 提及的LSTM通過更複雜的門控機制來改進的地方。

✍️ **Human**:



## 待解問題
非線性激活函數 `tanh` 在這裡扮演了什麼關鍵角色？如果使用ReLU等其他激活函數會有什麼影響？
