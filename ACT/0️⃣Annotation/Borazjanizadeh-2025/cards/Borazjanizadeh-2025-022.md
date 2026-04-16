---
title: "數據準備：句子分割 (Sentence Splitting)"
summary: |-
  "We preprocess the training corpora by first separating each document (a standalone Wikipedia article) based on title formatting, and then splitting text into sentences using the “SaTCapped” method."
---

## 說明
ThoughtGestalt (TG) 模型需要特定的數據準備流程。首先，訓練語料庫會根據標題格式分割成獨立的文檔單位（例如，單個維基百科文章）。接著，每個文檔中的文本會使用「SaTCapped」方法分割成句子。

SaTCapped方法能在詞元級別預測句子邊界，並對不完美的標點符號具有魯棒性。它還透過應用標點符號感知的回退規則，將超過最大詞元長度（實驗中設定為L=64詞元）的句子分割成更短、語義連貫的片段。選擇此方法是因為它在類似架構中實現了最高的AutoBLEU句子重構分數，確保了句子分割的質量。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-006]]


**導向** → [[Borazjanizadeh-2025-023]]




## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.1 Data Preparation)
- 🎯 **情境**: 描述了TG模型數據準備流程的第一步，強調了精確和語義連貫的句子分割對於模型性能的重要性，因為模型依賴於句子作為基本處理單元。

## 個人筆記


🤖 **AI**: 句子分割的質量對於TG模型的性能至關重要，因為 [[Borazjanizjan-2025-006]] 中提出的「句子級思想狀態」直接依賴於此。SaTCapped方法的選擇，特別是其對不完美標點的魯棒性和最大長度限制，顯示了對實際數據處理中常見問題的考量。然而，不同的分割方法對模型最終表現的敏感性仍值得深入探究。
✍️ **Human**:



## 待解問題
如果句子分割不夠精確，或者將語義不連貫的片段誤分為「句子」，將會如何影響TG模型學習到的句子表徵和整體性能？
