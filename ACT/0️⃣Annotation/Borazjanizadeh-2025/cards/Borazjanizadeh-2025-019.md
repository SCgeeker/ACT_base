---
title: "GPT-2 + Gist Masking 基線模型"
summary: |-
  "To test whether this attention-distribution mechanism can reproduce TG’s gain without recurrence or an external memory, we implement a GPT-2 baseline that (i) inserts <BOS>/<EOS> boundaries in the token stream and (ii) applies an additive attention-bias mask that restricts each token to attend causally within its own sentence, while accessing previous sentences only via each sentence’s last token, <EOS>, acting as a “gist” token."
---

## 說明
這項基線模型旨在探究ThoughtGestalt (TG) 模型中「注意力分佈機制」（即透過壓縮摘要向量訪問先前語境）的效果，是否能在沒有遞歸或外部記憶的情況下重現。該模型是標準GPT-2，但有兩個關鍵修改：(i) 在詞元流中插入<BOS>/<EOS>邊界；(ii) 應用一種附加注意力偏置掩碼，限制每個詞元僅在其所屬句子內進行因果注意力，而只能透過每個句子的末尾詞元<EOS>（作為「要旨詞元」）來訪問之前的句子。

儘管這種設計在注意力連接上模仿了TG的高層次模式，但它移除了遞歸和外部記憶。實驗結果顯示，該模型的性能遠不如標準GPT-2和TG，這表明當壓縮狀態無法可靠地語境化時，限制直接訪問先前詞元可能會放大錯誤，而非提升抽象能力。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-014]]




**對比** ⚡ [[Borazjanizadeh-2025-007]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (4.2 Other Baselines)
- 🎯 **情境**: 作為消融實驗的一部分，用來評估TG模型在注意力機制上的設計（即透過語義摘要訪問先前上下文）在沒有遞歸和外部記憶的情況下是否有效，並證明了TG模型中其他組件的重要性。

## 個人筆記


🤖 **AI**: GPT-2 + Gist Masking的失敗案例強調了「可靠語境化」的重要性。如果[[Borazjanizadeh-2025-014]]中提到的壓縮單元本身就不夠穩健或未經充分優化，那麼僅僅依靠注意力掩碼來引導模型關注這些單元，反而會引入噪音。這進一步突顯了[[Borazjanizadeh-2025-008]]中端到端梯度流對於優化句子表徵的關鍵作用。
✍️ **Human**:



## 待解問題
在沒有遞歸和外部記憶的情況下，是否存在其他方法能夠在Transformer內部有效地學習和利用「要旨」表徵，而不會導致性能下降？
