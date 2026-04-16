---
title: "TG模型對比 LCM 模型"
summary: |-
  "Large Concept Model (LCM) [44] similarly operates at the sentence level, but trains an autoregressive model to predict the next sentence embedding in a frozen SONAR representations space, which is then decoded into tokens, rather than directly predicting a token sequence."
---

## 說明
Large Concept Model (LCM) 是一個與ThoughtGestalt (TG) 模型在句子層次操作上相似的模型，但其具體方法有所不同。LCM訓練一個自動迴歸模型來預測預先定義的「SONAR表徵空間」中的下一個句子嵌入。這個SONAR表徵空間是**凍結的（frozen）**，即在訓練過程中不會更新其底層參數。然後，這些句子嵌入再被解碼回詞元。

相較之下，TG模型不使用凍結的編碼器或任何單獨的句子層次損失。TG的詞元和句子空間是共同學習的，僅使用單一的下一詞元預測目標進行監督。這種差異使得TG避免了輔助損失的脆弱性，同時仍能產生可重用作先前內容高層次狀態的語境化句子嵌入。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-006]]




**對比** ⚡ [[Borazjanizadeh-2025-013]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Other Works
- 🎯 **情境**: 在「其他工作」章節中，LCM模型作為與TG在句子層次處理上相似但方法不同的模型被介紹，凸顯了TG在表徵學習和訓練目標上的獨特優勢。

## 個人筆記


🤖 **AI**: LCM模型使用「凍結的表徵空間」雖然簡化了訓練，但也限制了表徵本身的學習能力，使其無法從最終的詞元預測任務中獲得直接的反饋。這與 [[Borazjanizadeh-2025-008]] 中TG強調的「端到端梯度流」形成了鮮明對比，也解釋了為何TG模型在數據和參數效率上能表現更優。
✍️ **Human**:



## 待解問題
凍結表徵空間與端到端學習之間，在不同任務和資源限制下，應如何選擇？是否可以設計一種混合方法，利用兩者的優勢？
