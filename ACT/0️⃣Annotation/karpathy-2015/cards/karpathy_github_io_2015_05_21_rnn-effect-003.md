---
title: "推翻「RNNs難以訓練」的傳統觀念"
summary: |-
  "What made this result so shocking at the time was that the common wisdom was that RNNs were supposed to be difficult to train (with more experience I’ve in fact reached the opposite conclusion)."
---

## 說明
作者指出，當時普遍認為循環神經網路（RNNs）是一種難以訓練的模型。然而，他在實踐中卻得出相反的結論：RNNs訓練起來實際上比預期中更容易，並且表現出強大的能力和穩定性（robustness）。
這種觀念上的轉變對於深度學習領域的發展至關重要，它促使研究人員和開發者重新評估RNNs的潛力，並投入更多資源進行研究和應用。這是一個從「理解」到「評估」層次的認知轉變。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-001]], [[karpathy_github_io_2015_05_21_rnn-effect-002]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-004]], [[karpathy_github_io_2015_05_21_rnn-effect-014]]




## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Introduction
- 🎯 **情境**: 作者在引言中提到其個人經驗與當時的普遍認知相悖，突出了RNNs的實際效用被低估的觀點。這為後續解釋RNNs的具體工作原理和應用場景做鋪墊，以證實其「非凡有效性」。

## 個人筆記


🤖 **AI**: 這種觀念轉變可能部分歸因於優化算法（如 [[karpathy_github_io_2015_05_21_rnn-effect-019]] 中的RMSProp或Adam）以及LSTM等改進型RNN架構的發展。難以訓練的說法，可能更多源於早期的梯度消失/爆炸問題，而非RNNs本身固有的缺陷。

✍️ **Human**:



## 待解問題
除了優化算法和LSTM之外，還有哪些因素促成了「RNNs難以訓練」觀念的改變？這種「容易訓練」的結論是否普遍適用於所有RNNs架構和任務？
