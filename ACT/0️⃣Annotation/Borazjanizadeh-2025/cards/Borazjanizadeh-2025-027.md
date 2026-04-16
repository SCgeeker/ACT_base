---
title: "可學習記憶門 (Learnable Memory Gates)"
summary: |-
  "Each cross-attention block has a scalar, learnable memory gate g(ℓ)mem that scales the cross-attention increment before it is added back via the residual path."
---

## 說明
ThoughtGestalt (TG) 模型在每個交叉注意力區塊中，都配備了一個標量且可學習的「記憶門」（memory gate）。這個記憶門 g(ℓ)mem 用於調整交叉注意力增量（cross-attention increment）的尺度，然後再透過殘差路徑將其加回。

這些記憶門允許模型在訓練過程中動態地調節對記憶路徑的依賴程度。例如，在訓練早期，當句子表徵尚不穩定或不夠信息量時，模型可能會下調對記憶的依賴；而一旦句子表徵變得穩定且豐富，模型則可能上調記憶的權重。這種自適應機制有助於模型在不同訓練階段更有效地利用記憶。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-007]]



**相關** ↔ [[Borazjanizadeh-2025-028]]



## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Main Design Principles (3.2 Model)
- 🎯 **情境**: 描述了TG模型中一個用於精細控制記憶信息流的組件，解釋了它如何幫助模型自適應地調整對外部記憶的依賴，以優化學習過程。

## 個人筆記


🤖 **AI**: 可學習記憶門的設計，為TG模型增加了靈活性和適應性。它允許模型在訓練過程中自主決定何時以及多大程度上信任其內部記憶，這對於 [[Borazjanizadeh-2025-008]] 中端到端梯度流的穩定性可能至關重要。這種自適應機制在學習過程中避免了過早地依賴不成熟的表徵。
✍️ **Human**:



## 待解問題
記憶門的學習曲線如何？它是否會導致模型在某些情況下過度依賴或忽略記憶信息？是否有必要引入更複雜的門控機制（例如，與LSTM類似的三個門）？
