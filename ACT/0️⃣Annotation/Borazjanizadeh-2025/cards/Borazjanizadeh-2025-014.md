---
title: "序列壓縮與摘要 (Sequence Compression and Gisting)"
summary: |-
  "Several recent approaches compress long token sequences into a small set of learned vectors. Gisting for LLMs inserts special “gist" tokens in context after the prompt and modifies attention masks so that gist tokens attend to the full prompt, while later tokens attend only to the gists, forcing the model to compress the prompt into a few gist representations that can be cached and reused [38]."
---

## 說明
為了處理長序列上下文，許多方法嘗試將冗長的詞元序列壓縮成一小組學習到的向量。例如，「Gisting for LLMs」透過在提示後插入特殊的「要旨詞元」（gist tokens），並修改注意力掩碼，使得要旨詞元關注整個提示，而後續詞元僅關注這些要旨。這迫使模型將提示信息壓縮到幾個可快取和重用的要旨表徵中。

AutoCompressors和Compressive Transformers也採用類似的思想，透過遞歸總結或分層記憶來實現長距離上下文的壓縮。這些方法旨在在不犧牲關鍵信息的情況下，減少模型處理長文本的計算負擔。

## 連結網絡




**相關** ↔ [[Borazjanizadeh-2025-007]], [[Borazjanizadeh-2025-015]]


**對比** ⚡ [[Borazjanizadeh-2025-019]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works
- 🎯 **情境**: 在「其他工作」章節中，作為與TG模型在處理長序列上下文方面相關的一類方法被介紹，突出了TG在壓縮機制上的獨特之處。

## 個人筆記


🤖 **AI**: 序列壓縮和Gisting是處理長文本的有效策略，但其關鍵挑戰是如何確保壓縮後的「要旨」能捕捉所有重要信息而不丟失細節。TG模型透過將句子視為語義連貫的單元來進行壓縮（參見 [[Borazjanizadeh-2025-007]]），這可能比單純基於詞元數量的壓縮更為有效和語義化。
✍️ **Human**:



## 待解問題
如何平衡壓縮的效率與信息的完整性？在壓縮過程中，模型是否會忽略某些在特定任務中至關重要的細節？
