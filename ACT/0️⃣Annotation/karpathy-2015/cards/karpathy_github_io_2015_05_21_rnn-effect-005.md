---
title: "傳統神經網路的固定輸入輸出限制"
summary: |-
  "A glaring limitation of Vanilla Neural Networks (and also Convolutional Networks) is that their API is too constrained: they accept a fixed-sized vector as input (e.g. an image) and produce a fixed-sized vector as output (e.g. probabilities of different classes)."
---

## 說明
傳統神經網路，包括香草神經網路（Vanilla Neural Networks）和卷積神經網路（Convolutional Networks），存在一個明顯的局限性：它們的介面（API）過於受限，只能接受固定大小的向量作為輸入（例如圖像），並產生固定大小的向量作為輸出（例如不同類別的概率）。
這種固定大小的輸入輸出限制了它們在處理可變長度序列數據（如文本、語音）方面的應用，這正是循環神經網路（RNNs）能夠超越傳統模型的關鍵原因。
此概念屬於「理解」和「分析」層次，用於對比不同網路架構的特性。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-004]]




**對比** ⚡ [[karpathy_github_io_2015_05_21_rnn-effect-004]]


## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Recurrent Neural Networks
- 🎯 **情境**: 在解釋循環網路的特殊之處時，作者首先闡述了傳統神經網路的局限性，以此凸顯RNNs處理序列數據能力的優勢。

## 個人筆記


🤖 **AI**: 雖然傳統網路有固定輸入輸出的限制，但在許多領域（如圖像分類）它們仍非常有效。這種限制促使了新的架構發展，但也值得思考，是否所有問題都必須以序列方式處理？例如，Transformer架構雖然處理序列，但其核心並非RNN的循環機制，這與 [[karpathy_github_io_2015_05_21_rnn-effect-004]] 所強調的RNN核心優勢形成有趣的對比。

✍️ **Human**:



## 待解問題
有沒有辦法在不改變傳統神經網路固定輸入輸出結構的前提下，間接地處理序列數據？
