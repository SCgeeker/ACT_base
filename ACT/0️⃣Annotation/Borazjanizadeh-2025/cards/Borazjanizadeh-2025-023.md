---
title: "數據準備：句子詞元化與特殊標記"
summary: |-
  "Following sentence splitting, each sentence is tokenized, padded to the set maximum length L, and enclosed by special boundary markers: a start-of-sentence token (<BOS>) and an end-of-sentence token (<EOS>)."
---

## 說明
在句子分割之後，ThoughtGestalt (TG) 模型的數據準備流程進一步包括詞元化和添加特殊標記。每個分割出的句子會被詞元化，然後填充到預設的最大長度L，並用特殊的邊界標記包圍：一個句子開始詞元（<BOS>）和一個句子結束詞元（<EOS>）。

<BOS>詞元使TG模型能夠預測新句子的第一個詞彙詞元，並設定非空語境以啟用對句子記憶的交叉注意力。而<EOS>詞元則標誌著句子生成的結束，並作為提取句子表徵隱藏狀態的指定位置。對於文檔的最後一個句子，還會在其<EOS>之前附加一個<EOD>標記，以指示文本生成的結束。這些標記確保了模型能夠明確識別句子邊界並執行相應的操作。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-022]]


**導向** → [[Borazjanizadeh-2025-024]]


**相關** ↔ [[Borazjanizadeh-2025-026]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.1 Data Preparation)
- 🎯 **情境**: 描述了TG模型數據準備流程的第二步，詳細說明了如何將句子轉換為模型可處理的輸入格式，並解釋了特殊標記的功能。

## 個人筆記


🤖 **AI**: 特殊標記<BOS>和<EOS>在TG模型中扮演著雙重角色：不僅作為結構性邊界指示符，更是生成新句子和提取句子表徵的關鍵信號。這種明確的語義和功能綁定，使得模型能夠更好地利用這些邊界信息，這與 [[Borazjanizadeh-2025-017]] 中單純將邊界作為「偏差」的GPT-2基線模型有本質區別。
✍️ **Human**:



## 待解問題
特殊標記的選擇和其在詞彙表中的位置會對模型學習產生什麼影響？如果去除某些特殊標記，模型性能會如何變化？
