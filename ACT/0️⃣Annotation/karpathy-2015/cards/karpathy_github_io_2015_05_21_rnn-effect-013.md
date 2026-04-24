---
title: "深度循環網路：堆疊模型以提升性能"
summary: |-
  "RNNs are neural networks and everything works monotonically better (if done right) if you put on your deep learning hat and start stacking models up like pancakes."
---

## 說明
像其他神經網路一樣，循環神經網路（RNNs）的性能可以透過堆疊多個層次來提升，形成深度循環網路。這種方法被比喻為「像煎餅一樣堆疊模型」。
在這種架構中，一個RNN的輸出作為下一個RNN的輸入，使得模型能夠學習更複雜、更高層次的抽象表示。例如，一個2層的循環網路可以由 `y1 = rnn1.step(x)` 和 `y = rnn2.step(y1)` 組成。
此概念屬於「應用」和「創造」層次，展示了RNNs模型設計的擴展性。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-009]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-014]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-024]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Going deep
- 🎯 **情境**: 在解釋了單個RNN的工作原理後，作者進一步介紹了如何透過堆疊多層RNN來構建更強大的模型，這是深度學習的普遍實踐，並將其應用於RNNs。

## 個人筆記


🤖 **AI**: 堆疊RNNs可以增加模型的容量和表達能力，但同時也增加了訓練的複雜性和計算成本。這使得像 [[karpathy_github_io_2015_05_21_rnn-effect-019]] 中提到的高級優化器變得更加重要。此外，層數的增加也可能加劇梯度消失/爆炸問題，需要LSTM等更穩定的單元設計來緩解。

✍️ **Human**:



## 待解問題
堆疊多少層的RNN才算「最佳」？是否存在堆疊層數過多導致性能下降或訓練困難的臨界點？
