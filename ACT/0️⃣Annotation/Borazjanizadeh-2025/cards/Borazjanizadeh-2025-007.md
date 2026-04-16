---
title: "句子級「思想」狀態與遞歸記憶"
summary: |-
  "TG predicts the tokens of one sentence at a time while cross-attending to a memory of prior sentence representations."
---

## 說明
ThoughtGestalt (TG) 模型的核心運作方式是遞歸地處理語言。它一次生成一個句子的所有詞元，並且在生成這些詞元的過程中，會執行「交叉注意力」操作，去關注一個儲存了先前句子表徵的記憶模塊。這個記憶模塊扮演著長期語境的角色。

這種機制使得模型能夠在處理當前句子時，不僅依賴於當前句子的局部信息和內部自注意力，還能有效整合來自過去句子的更高層次語義信息。每個句子表徵都是一個「整體概念」（gestalt），捕捉了該句子的全面意義，並在處理完畢後被寫入記憶以供後續使用。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-006]]


**導向** → [[Borazjanizadeh-2025-008]], [[Borazjanizadeh-2025-010]]


**相關** ↔ [[Borazjanizadeh-2025-014]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Abstract, Introduction, Main Design Principles
- 🎯 **情境**: 描述TG模型的核心運行流程和其創新的記憶機制，解釋了如何透過遞歸和交叉注意力整合句子級語境信息。

## 個人筆記


🤖 **AI**: 將句子表徵儲存到記憶中並透過交叉注意力機制引用，是TG模型突破傳統Transformer線性限制的關鍵。這種方式有望解決 [[Borazjanizadeh-2025-003]] 中提到的語境化錯誤，因為模型總能存取到已完全語境化的高層次信息。
✍️ **Human**:



## 待解問題
記憶模塊中儲存的句子表徵會隨著時間推移而衰減或被更新嗎？如何管理這種長期記憶以避免信息過載和衝突？
