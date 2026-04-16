---
title: "父子關係探測 (Father–Son Reversal Curse Probe)"
summary: |-
  "We evaluate the robustness of TG and GPT-2 to the in-context reversal curse using a controlled Father–Son relation probe in completion mode."
---

## 說明
父子關係探測是一種實驗方法，用於評估語言模型對「反轉詛咒」（reversal curse）現象的魯棒性。在完成模式下，每個測試範例包含一個建立關係的上下文句子（例如：「Michael的兒子是John」），後跟一個查詢前綴。

實驗分為兩種條件：正常條件下，查詢重複關係陳述（例如：「Michael的兒子是」），期望模型完成「John」。反向條件下，查詢反轉了關係方向（例如：「John的父親是」），期望模型完成「Michael」。透過比較模型在這兩種條件下的表現，尤其是在反向條件下的負對數似然（NLL），可以量化模型對關係方向的理解和泛化能力。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-002]]


**導向** → [[Borazjanizadeh-2025-011]]




## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (4.3 Reversal curse evaluation (Father–Son completion))
- 🎯 **情境**: 描述了用於評估TG模型在關係方向泛化能力上的具體實驗方法和設置，為理解其在反轉詛咒方面的改進提供了背景。

## 個人筆記


🤖 **AI**: 這種探測方法提供了一個清晰且受控的環境來評估模型對關係的語義理解。然而，現實世界中的關係可能更為複雜和多樣，例如多重關係、間接關係等。未來可以設計更複雜的探測來測試模型在更廣泛的關係推理場景下的能力，這將為 [[Borazjanizadeh-2025-011]] 的發現提供更全面的驗證。
✍️ **Human**:



## 待解問題
除了父子關係，是否還有其他具代表性的關係類型可以設計成類似的探測，以全面評估模型的關係推理能力？如何確保探測的語句結構不會對模型造成額外的偏見？
