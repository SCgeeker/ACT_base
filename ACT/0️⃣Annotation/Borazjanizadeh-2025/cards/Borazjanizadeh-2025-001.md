---
title: "傳統Transformer語言模型的核心限制"
summary: |-
  "However, standard Transformers represent context primarily as token embeddings tied to positional indices; consequently, the model’s internal state is inherently coupled to linear word order."
---

## 說明
傳統Transformer語言模型，例如GPT系列，主要將語言視為詞元序列，並透過學習大規模語料庫中的表面層次共現統計來預測下一個詞元。這種方法雖然在生成流暢文本方面取得了顯著成功，但其內部狀態本質上與線性的詞序緊密耦合。

這導致模型難以形成全局一致的潛在實體和事件表徵，因為它主要依賴於詞元嵌入及其位置索引來表示語境。這種詞元中心的方法限制了模型在需要深層語義理解、關係推理和長距離上下文整合的複雜任務中的表現。

## 連結網絡



**導向** → [[Borazjanizadeh-2025-002]], [[Borazjanizadeh-2025-003]]



**對比** ⚡ [[Borazjanizadeh-2025-005]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Introduction
- 🎯 **情境**: 在介紹現有大型語言模型（LLMs）的成功及其固有局限性時提出，為作者引入其研究動機和ThoughtGestalt模型奠定基礎。

## 個人筆記


🤖 **AI**: 傳統Transformer模型對線性詞序的依賴，雖然在序列建模上有效，但顯然限制了對抽象語義的捕捉。這使得模型在處理如 [[Borazjanizadeh-2025-002]] 中提到的「反轉詛咒」等語義推理任務時表現脆弱。
✍️ **Human**:



## 待解問題
如何設計語言模型，使其內部狀態能夠超越單純的線性詞序，更有效地捕捉和表示高層次的語義結構？
