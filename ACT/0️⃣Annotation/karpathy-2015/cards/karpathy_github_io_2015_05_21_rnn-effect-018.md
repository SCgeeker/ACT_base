---
title: "Softmax分類器與交叉熵損失"
summary: |-
  "A more technical explanation is that we use the standard Softmax classifier (also commonly referred to as the cross-entropy loss) on every output vector simultaneously."
---

## 說明
在循環神經網路（RNN）的字符級語言模型訓練中，每個時間步的輸出向量會同時應用標準的Softmax分類器。Softmax函數將RNN輸出的原始置信度（logits）轉換為介於0到1之間且總和為1的概率分佈，代表了每個可能字符作為下一個字符的概率。
同時，訓練過程採用交叉熵損失（cross-entropy loss）來衡量模型預測的概率分佈與真實目標字符分佈之間的差異。優化目標是最小化這個損失，從而使模型預測的概率分佈盡可能接近真實分佈。
此概念屬於「應用」和「分析」層次，是RNN訓練中的核心優化機制。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-017]], [[karpathy_github_io_2015_05_21_rnn-effect-012]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-019]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-023]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Character-Level Language Models
- 🎯 **情境**: 在解釋RNN如何將輸出置信度轉化為可訓練的概率並衡量預測誤差時，作者引入了Softmax分類器和交叉熵損失，這是所有分類問題的標準做法。

## 個人筆記


🤖 **AI**: Softmax和交叉熵損失是標準的分類任務組件，其在字符級語言模型中的應用確保了訓練的穩定性和有效性。然而，對於非常大的詞彙表，Softmax計算成本可能會很高。這種標準方法與 [[karpathy_github_io_2015_05_21_rnn-effect-012]] 中描述的「尋找最佳權重」目標密切相關，因為它提供了衡量「最佳」的量化方式。

✍️ **Human**:



## 待解問題
在極端不平衡的字符分佈情況下，交叉熵損失是否仍然是最佳選擇？是否有更魯棒的損失函數？
