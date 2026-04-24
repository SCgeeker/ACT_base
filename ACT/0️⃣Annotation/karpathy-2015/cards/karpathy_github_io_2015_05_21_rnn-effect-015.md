---
title: "字符級語言模型（Character-Level Language Models）"
summary: |-
  "That is, we’ll give the RNN a huge chunk of text and ask it to model the probability distribution of the next character in the sequence given a sequence of previous characters. This will then allow us to generate new text one character at a time."
---

## 說明
字符級語言模型（Character-Level Language Models）是一種讓循環神經網路（RNNs）透過學習文本數據來預測序列中下一個字符概率分佈的應用。模型接收大量文本作為輸入，並學會根據前面字符的序列來預測最可能出現的下一個字符。
這種模型的核心用途是生成全新的文本，其方式是每次生成一個字符，然後將生成的字符作為下一個時間步的輸入，如此循環。
此概念屬於「應用」和「創造」層次，是RNNs在文本生成領域的經典應用之一。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-004]], [[karpathy_github_io_2015_05_21_rnn-effect-014]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-016]], [[karpathy_github_io_2015_05_21_rnn-effect-017]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-021]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Character-Level Language Models
- 🎯 **情境**: 作者在解釋完RNNs的基本原理和LSTM的優勢後，引入了字符級語言模型作為一個具體的、有趣的應用實例，用以展示RNNs的實際效果。

## 個人筆記


🤖 **AI**: 字符級語言模型的一個挑戰是處理長距離語義和語法結構，儘管LSTM有所改進，但其記憶容量仍有限。例如，在 [[karpathy_github_io_2015_05_21_rnn-effect-028]] 中，模型在生成代碼時無法有效跟蹤變量名，這就顯示了在複雜結構中，即便預測了下一個字符，也難以維持整體邏輯連貫性。

✍️ **Human**:



## 待解問題
字符級語言模型在生成長篇文本時，如何確保文本的語義連貫性和邏輯一致性？它與詞級語言模型相比有何優劣？
