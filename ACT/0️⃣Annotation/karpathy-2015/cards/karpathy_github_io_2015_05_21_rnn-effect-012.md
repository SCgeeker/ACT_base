---
title: "RNN訓練的目標：尋找最佳權重矩陣"
summary: |-
  "We initialize the matrices of the RNN with random numbers and the bulk of work during training goes into finding the matrices that give rise to desirable behavior, as measured with some loss function that expresses your preference to what kinds of outputs y you’d like to see in response to your input sequences x."
---

## 說明
RNN訓練的核心目標是找到一組能夠產生期望行為的權重矩陣（即 `W_hh`, `W_xh`, `W_hy` 等參數）。這些矩陣最初被隨機初始化。訓練過程中，模型會根據某種損失函數（loss function）來衡量其輸出 `y` 與期望輸出之間的差異，並據此調整權重。
損失函數定義了我們對模型輸出的偏好，例如在文本生成中，我們希望模型能預測正確的下一個字符。優化算法（如梯度下降）將會最小化這個損失，從而使模型的行為逐步趨近於期望。
此概念屬於「理解」和「應用」層次，闡明了RNN訓練的基礎。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-011]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-018]], [[karpathy_github_io_2015_05_21_rnn-effect-019]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-007]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: RNN computation
- 🎯 **情境**: 在解釋RNNs的內部運算和參數構成後，作者進一步說明了訓練過程的本質，即透過優化找到最佳的權重矩陣以實現期望的輸出行為。

## 個人筆記


🤖 **AI**: 損失函數的選擇對於訓練結果至關重要，它直接決定了模型「期望行為」的定義。在字符級語言模型中，交叉熵損失（cross-entropy loss）是常見選擇，這與 [[karpathy_github_io_2015_05_21_rnn-effect-018]] 中提到的Softmax分類器密切相關。然而，設計一個好的損失函數來捕捉複雜行為（如風格、語義）仍是一個挑戰。

✍️ **Human**:



## 待解問題
如何設計一個能夠有效捕捉複雜行為（如創造力或上下文理解）的損失函數，而不僅僅是簡單的預測準確性？
