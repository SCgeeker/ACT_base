---
title: "RNN透過循環連接追蹤上下文"
summary: |-
  "The RNN therefore cannot rely on the input alone and must use its recurrent connection to keep track of the context to achieve this task."
---

## 說明
循環神經網路（RNN）的設計使其不僅依賴於當前的輸入，更重要的是，它必須利用其循環連接（recurrent connection）來追蹤和維持上下文信息。這使得RNN能夠理解序列中字符的意義是依賴於其歷史背景的。
作者以「hello」為例，說明了即使是相同的輸入字符「l」，其後期望的目標字符卻不同（第一次是「l」，第二次是「o」）。這證明了RNN必須具備「記憶」上下文的能力，而不能僅憑單一輸入來做判斷。
此概念屬於「理解」和「分析」層次，闡明了RNN獨特的記憶機制。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-004]], [[karpathy_github_io_2015_05_21_rnn-effect-009]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-021]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-014]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Character-Level Language Models
- 🎯 **情境**: 在解釋字符級語言模型的訓練過程時，作者特別指出RNNs不能僅依賴單個輸入，而必須利用其循環結構來維護上下文，這是RNN處理序列任務的內在需求。

## 個人筆記


🤖 **AI**: 循環連接是RNNs的核心特徵，使其能夠處理時間依賴性。然而，這種機制在長期上下文追蹤上仍有其局限性，導致梯度消失問題。這也正是 [[karpathy_github_io_2015_05_21_rnn-effect-014]] 中LSTM等改進型架構誕生的原因，它們通過更精巧的門控來優化上下文信息的流動。

✍️ **Human**:



## 待解問題
RNN的循環連接在處理多長時間的上下文時會開始失效？如何量化其「記憶」能力？
