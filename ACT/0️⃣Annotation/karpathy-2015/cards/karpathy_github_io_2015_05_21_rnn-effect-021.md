---
title: "測試時透過採樣生成文本"
summary: |-
  "At test time, we feed a character into the RNN and get a distribution over what characters are likely to come next. We sample from this distribution, and feed it right back in to get the next letter. Repeat this process and you’re sampling text!"
---

## 說明
在循環神經網路（RNN）的測試或推理階段，生成文本的過程是透過連續採樣完成的。首先，將一個初始字符（或序列）輸入到RNN中，模型會輸出一個預測下一個字符的概率分佈。
接著，不是直接選擇概率最高的字符，而是從這個概率分佈中進行採樣，得到一個實際的下一個字符。這個被採樣得到的字符隨後會作為新的輸入，再次餵入RNN，以預測再下一個字符的概率分佈。這個遞歸的過程不斷重複，直到生成所需長度的文本。
此概念屬於「應用」和「創造」層次，說明了RNN如何從訓練模型中產生新內容。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-017]], [[karpathy_github_io_2015_05_21_rnn-effect-018]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-022]], [[karpathy_github_io_2015_05_21_rnn-effect-023]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-015]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Character-Level Language Models
- 🎯 **情境**: 在解釋完RNN字符級語言模型的訓練過程後，作者詳細描述了如何利用訓練好的模型來實際生成新文本，這是該應用最直觀的體現。

## 個人筆記


🤖 **AI**: 這種遞歸採樣方法是文本生成的核心，但其生成的文本質量（如連貫性和創造性）很大程度上取決於採樣策略。例如，當 [[karpathy_github_io_2015_05_21_rnn-effect-023]] 描述的溫度參數設定很低時，採樣會變得保守，可能導致重複循環。這凸顯了採樣策略在平衡創造性和可讀性之間的重要性。

✍️ **Human**:



## 待解問題
除了簡單的隨機採樣，還有哪些更複雜或更優雅的採樣策略可以提高生成文本的質量？如何避免生成重複或無意義的文本段落？
