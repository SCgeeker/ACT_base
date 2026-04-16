---
title: "訓練日程：句子流課程學習 (Sentence-stream Curriculum)"
summary: |-
  "We address this with a curriculum over the maximum sentence-stream length S used to slice training documents: we begin with shorter streams and periodically increase S and re-chunk the training split (validation and test sets are never split into sentence streams)."
---

## 說明
ThoughtGestalt (TG) 模型在訓練中採用了一種「句子流課程學習」的策略，以管理計算圖的深度和優化難度。由於保留記憶寫入的計算圖會導致有效的反向傳播深度隨連續處理的句子數量而增長，因此在訓練早期，句子表徵可能不夠信息豐富。過長的句子流會增加計算和優化難度，卻無法提供有用的長距離信用分配。

為此，研究中對用於切割訓練文檔的最大句子流長度S實施了課程學習：訓練從較短的句子流開始，並每隔5個epoch定期增加S的值（例如，從S=30開始，每次增加12個句子）。這種漸進式增加S的策略，使早期優化專注於句子內的詞元建模和短距離記憶利用，同時逐步擴展有效依賴範圍。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-024]]



**相關** ↔ [[Borazjanizadeh-2025-030]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.3 Training schedules)
- 🎯 **情境**: 描述了TG模型訓練過程中的一個關鍵策略，用以平衡計算複雜度與學習長距離依賴的需求，確保訓練的穩定性和效率。

## 個人筆記


🤖 **AI**: 句子流課程學習是TG模型在實際訓練中解決計算圖複雜度和信息質量不確定性問題的實用策略。它體現了循序漸進的學習思想，先從簡單、局部的信息開始學習，再逐漸擴展到複雜、長距離的依賴。這與 [[Borazjanizadeh-2025-024]] 中提到的句子流處理方式緊密配合，共同提高了訓練效率和模型的穩健性。
✍️ **Human**:



## 待解問題
句子流長度S的增加步長和頻率如何影響訓練的收斂速度和模型的最終性能？是否存在一種自適應的課程學習機制，能夠根據模型學習進度動態調整S？
