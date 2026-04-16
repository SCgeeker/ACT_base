---
title: "反轉詛咒 (Reversal Curse)"
summary: |-
  "Similarly, the reversal curse shows that models trained on "A is B" often fail to infer "B is A," treating the two directions of a relational fact as distinct statistical patterns rather than a unified semantic relation."
---

## 說明
反轉詛咒是大型語言模型（LLMs）普遍存在的脆弱性之一，指模型在學習了單向關係（例如「A是B的父親」）後，難以推斷出其反向關係（「B是A的兒子」）。這表明模型傾向於將關係的兩個方向視為兩個獨立的、表層的統計模式，而非一個統一且可逆的語義事實。

這種現象反映了LLMs在構建全局一致的潛在知識表徵方面的不足，它們難以抽象出超越表面詞元共現的深層語義關係。這對於模型在知識圖譜推理、問答系統等需要理解關係方向的任務中構成挑戰。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-001]]


**導向** → [[Borazjanizadeh-2025-012]]


**相關** ↔ [[Borazjanizjan-2025-003]]


**對比** ⚡ [[Borazjanizadeh-2025-011]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Introduction
- 🎯 **情境**: 作為現有大型語言模型（LLMs）在關係方向理解上存在根本性缺陷的具體例子，強調了其「詞元中心」方法的局限性，引導讀者理解本研究引入高層次抽象的必要性。

## 個人筆記


🤖 **AI**: 反轉詛咒的現象凸顯了目前LLMs的知識表徵可能過於碎片化且缺乏抽象性。雖然模型可能記住了大量的關係實例，但如果不能將其歸納為更通用的語義規則，那麼其在知識推理上的能力將大打折扣。這與 [[Borazjanizadeh-2025-001]] 提到的模型內部狀態與線性詞序耦合問題是同一枚硬幣的兩面。
✍️ **Human**:



## 待解問題
如何設計訓練機制，使模型能夠內化關係的語義對稱性或反向性，而非僅記憶表層的統計模式？
