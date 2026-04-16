---
title: "GPT-2與句子邊界偏差 (Sentence Boundary Bias)"
summary: |-
  "Figure 5(left) shows that inducing sentence boundary bias improves GPT-2 performance across all datasets sizes, with the most significant gains in the low-data regime (test PPL decreases 38.1→36.6 at 20M; see Table 3)."
---

## 說明
為了探究單純將句子邊界信息顯式地引入詞元流對標準Transformer模型的影響，研究中建立了一個GPT-2基準模型，並加入了句子邊界偏差。這項實驗將TG數據預處理管道生成的句子分割結果（包含<BOS>和<EOS>標記）扁平化為連續序列，輸入到標準GPT-2模型中。

結果顯示，引入這些特殊邊界詞元確實改善了GPT-2的性能，尤其是在數據量較少的訓練階段，困惑度有顯著下降。然而，這種改進隨著數據規模的增加而減小，並且TG模型在數據充足時能夠超越這個帶有邊界偏差的GPT-2。這表明單純的結構性偏差有益，但不足以複製TG從上下文語境化句子級潛在狀態中獲得的效率增益。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-006]]




**對比** ⚡ [[Borazjanizadeh-2025-009]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (4.2 Other Baselines)
- 🎯 **情境**: 作為對照實驗之一，用來隔離TG模型中「句子邊界作為結構偏差」這一特定設計的影響，以證明TG模型的增益不僅僅來自顯式標記句子邊界。

## 個人筆記


🤖 **AI**: GPT-2引入句子邊界偏差後性能的提升，說明了顯式結構信息對模型理解語言的重要性。然而，這種提升的邊際效益遞減，也間接支持了 [[Borazjanizadeh-2025-006]] 中「思想狀態」層次抽象的必要性：僅僅標記邊界是不足的，更重要的是在這些邊界處進行有意義的語義壓縮和表徵學習。
✍️ **Human**:



## 待解問題
除了<BOS>/<EOS>，是否還有其他方式可以有效地將語言的結構性邊界信息（如段落、篇章）傳遞給LLMs，並評估其影響？
