---
title: "Transformer中的遞歸與記憶 (Recurrence and Memory)"
summary: |-
  "Another design axis concerns extending Transformers to reuse past representations to enable accessing content beyond a fixed context window. Transformer-XL caches hidden states from previous segments and lets the current segment attend to them, providing segment-level recurrence but truncating gradients at the cached states [47]."
---

## 說明
Transformer模型最初被設計為處理固定長度的上下文窗口。為了超越這一限制並處理更長的序列，研究者們探索了在Transformer中引入遞歸和記憶機制。例如，Transformer-XL透過快取前一個區段的隱藏狀態，讓當前區段能夠關注這些快取狀態，從而實現了區段級的遞歸。

然而，許多這類方法在快取狀態處截斷了梯度流，導致無法進行端到端的優化。其他方法如Block-Recurrent Transformers和Recurrent Memory Transformer則引入了專門的記憶詞元或遞歸狀態來攜帶跨區塊信息，以提高長距離依賴的處理能力。

## 連結網絡




**相關** ↔ [[Borazjanizadeh-2025-014]]


**對比** ⚡ [[Borazjanizadeh-2025-016]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works
- 🎯 **情境**: 在比較其他相關工作時，作為解決Transformer長上下文問題的一類通用方法被介紹，為讀者理解TG模型在記憶和遞歸設計上的獨特之處提供了背景。

## 個人筆記


🤖 **AI**: 許多遞歸Transformer模型在快取狀態處截斷梯度的做法，雖然簡化了計算，但也可能限制了長期依賴的學習深度。TG模型在 [[Borazjanizadeh-2025-008]] 中強調的「保留計算圖」以實現端到端梯度流，正是為了克服這一局限性，這可能是其性能優於許多遞歸模型的關鍵。
✍️ **Human**:



## 待解問題
在保持梯度流動的同時，如何高效管理記憶中的大量隱藏狀態，避免內存爆炸和計算成本過高？不同的記憶機制（快取、記憶詞元、外部知識庫）在性能和效率上各有何優劣？
