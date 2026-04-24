---
title: "RNNs作為可程式化系統"
summary: |-
  "Viewed this way, RNNs essentially describe programs. In fact, it is known that RNNs are Turing-Complete in the sense that they can to simulate arbitrary programs (with proper weights)."
---

## 說明
循環神經網路（RNNs）可以被視為一種程式（programs）。它們將輸入向量與其內部狀態向量通過一個固定但可學習的函數相結合，產生新的狀態向量。這種運作方式類似於運行一個帶有輸入和內部變量的程式。
更進一步地，RNNs被證明是圖靈完備（Turing-Complete）的，這意味著在擁有適當權重的情況下，它們能夠模擬任何任意程式。這突顯了RNNs作為強大計算模型的潛力，超越了簡單的模式識別。
此概念屬於「理解」和「分析」層次，深入闡釋了RNNs的理論計算能力。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-004]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-007]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-009]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Recurrent Neural Networks
- 🎯 **情境**: 在討論RNNs處理序列的強大能力時，作者進一步將其提升到「程式」和「圖靈完備」的層面，以強調其潛在的通用計算能力，儘管也提醒讀者不要過度解讀。

## 個人筆記


🤖 **AI**: 將RNNs視為「程式」提供了一個有用的高層次抽象，幫助理解其動態行為。然而，「圖靈完備」是一個理論上限，在實際應用中，RNNs的性能和訓練複雜度仍受限於計算資源和優化算法。例如，雖然 [[karpathy_github_io_2015_05_21_rnn-effect-027]] 指出了RNNs在長期依賴上的問題，這與其理論上的圖靈完備性存在實際性能差距。

✍️ **Human**:



## 待解問題
如何在不犧牲訓練可行性的前提下，充分利用RNNs的圖靈完備特性來解決更複雜的計算問題？
