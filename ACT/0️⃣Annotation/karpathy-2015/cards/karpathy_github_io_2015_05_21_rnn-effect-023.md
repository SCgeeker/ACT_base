---
title: "採樣溫度（Temperature）對文本生成的影響"
summary: |-
  "Decreasing the temperature from 1 to some lower number (e.g. 0.5) makes the RNN more confident, but also more conservative in its samples. Conversely, higher temperatures will give more diversity but at cost of more mistakes (e.g. spelling mistakes, etc)."
---

## 說明
在文本生成過程中，Softmax函數的「溫度」（Temperature）參數可以被調整，以控制生成文本的特性。
*   降低溫度（例如從1降至0.5）會使RNN的預測更加自信和保守，傾向於選擇概率最高的字符，導致生成文本的多樣性降低，但語法錯誤減少。
*   升高溫度則會增加生成文本的多樣性，讓RNN有更大的機會選擇概率較低的字符，但代價是可能出現更多的錯誤，例如拼寫錯誤或語法不通順。
此參數提供了一種在生成文本的創造性與正確性之間取得平衡的機制。
此概念屬於「應用」和「評估」層次，影響文本生成行為。

## 連結網絡


**基於** → [[karpathy_github_io_2015_05_21_rnn-effect-021]]


**導向** → [[karpathy_github_io_2015_05_21_rnn-effect-022]]


**相關** ↔ [[karpathy_github_io_2015_05_21_rnn-effect-018]]



## 來源脈絡
- 📄 **文獻**: https://karpathy.github.io/2015/05/21/rnn-effectiveness/
- 📍 **位置**: Fun with RNNs / Paul Graham generator
- 🎯 **情境**: 在展示Paul Graham文本生成器後，作者介紹了如何透過調整採樣溫度來影響生成文本的風格和質量，這是一個重要的測試時參數。

## 個人筆記


🤖 **AI**: 溫度參數為生成模型提供了一個簡單而有效的控制機制，以權衡創造性和保守性。然而，過低的溫度可能導致模型陷入循環（如Paul Graham示例所示），而過高的溫度則會產生無意義的亂碼。這表明，即使模型本身表現出色，外部控制參數的選擇也極為關鍵，與 [[karpathy_github_io_2015_05_21_rnn-effect-002]] 中提到的超參數選擇對訓練初期效果的影響形成對比。

✍️ **Human**:



## 待解問題
是否存在一種動態調整溫度的策略，使其在不同生成階段都能保持最佳平衡？如何根據特定任務需求選擇合適的溫度？
