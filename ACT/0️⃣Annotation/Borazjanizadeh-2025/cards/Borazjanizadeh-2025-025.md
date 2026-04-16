---
title: "句子向量提取與句子頭 (Sentence Vector Extraction and Sentence Head)"
summary: |-
  "At a fixed mid layer ℓs (we use ℓs = 7), we form the sentence vector mt = Wsent H(ℓs) iEOS ∈ Rd. Here Wsent denotes the sentence head, which is a single linear layer Wsent ∈ Rd×d (depth 1)."
---

## 說明
在ThoughtGestalt (TG) 模型中，每個句子的「整體概念」（gestalt）是透過一個稱為「句子頭」（sentence head）的機制提取的。具體來說，在處理完一個句子後，會在一個固定的中間層ℓs（實驗中選定為第7層）的句子結束詞元（<EOS>）位置，提取其隱藏狀態H(ℓs)。然後，這個隱藏狀態會透過一個單獨的線性層Wsent進行投影，從而生成該句子的句子向量mt。

選擇從中間層提取句子表徵是基於先前的證據，這些證據表明Transformer模型的中間層通常攜帶最具上下文相關性和可遷移性的特徵，而頂層則更專注於詞元級別的決策（例如，下一詞元詞彙化）。這種設計確保了句子向量能捕捉到高層次的語義信息。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-006]], [[Borazjanizadeh-2025-023]]


**導向** → [[Borazjanizadeh-2025-007]]


**相關** ↔ [[Borazjanizadeh-2025-028]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.2 Model)
- 🎯 **情境**: 詳細描述了TG模型如何從內部處理過程中提取出代表句子整體意義的向量，這是其構建高層次記憶的關鍵步驟。

## 個人筆記


🤖 **AI**: 從中間層提取句子向量而非頂層，是一個深思熟慮的設計選擇，它利用了Transformer層次結構中信息流的特性。這與 [[Borazjanizadeh-2025-005]] 中提到的「整體概念」相符，因為中間層更可能包含融合了語法和語義的抽象信息。然而，最佳提取層的選擇是否會因任務或數據集而異，仍是一個值得研究的問題。
✍️ **Human**:



## 待解問題
如何系統性地確定提取句子表徵的最佳層次？這種提取機制對模型的泛化能力和解釋性有何影響？
