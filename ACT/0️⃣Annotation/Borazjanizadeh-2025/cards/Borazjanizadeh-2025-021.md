---
title: "外部記憶與上下文內記憶 (External vs. In-context Memory)"
summary: |-
  "Placing sentence vectors in context as a prefix and relying on self-attention across the extended sequence (while preserving gradient flow through the memory vectors) largely retains TG’s modeling benefits (test PPL 30.2), but is slower (throughput 19 vs. 21 sent./sec)."
---

## 說明
這項消融實驗比較了ThoughtGestalt (TG) 模型將句子向量儲存在「外部記憶」與作為「上下文前綴」（in-context）兩種方式的差異。當將句子向量作為上下文前綴放置，並透過擴展序列上的自注意力來處理時（同時保留梯度流通過記憶向量），模型仍能大致保留TG的建模優勢（測試困惑度為30.2）。

然而，這種上下文內記憶的方式訓練速度較慢（吞吐量為19句/秒，而外部記憶為21句/秒）。這符合自注意力機制計算成本的二次方特性：TG將處理分解為O(T²)的自注意力和O(T·M)的交叉注意力，而上下文內方法則對O((T+M)²)的連接序列進行自注意力計算，其中T是句子長度，M是記憶容量。這表明，雖然兩者都能實現良好的性能，但外部記憶在計算效率上更具優勢。

## 連結網絡


**基於** → [[Borazjanizadeh-2025-007]], [[Borazjanizadeh-2025-020]]




**對比** ⚡ [[Borazjanizadeh-2025-014]]


## 來源脈絡
- 📄 **文獻**: Borazjanizadeh-2025
- 📍 **位置**: Results (4.4 Ablations)
- 🎯 **情境**: 作為消融實驗的一部分，用以比較TG模型將句子表徵儲存於外部記憶的效率優勢，與將其作為上下文內前綴處理的性能和計算成本。

## 個人筆記


🤖 **AI**: 這項實驗結果再次驗證了計算效率在模型設計中的重要性。雖然將所有信息放在上下文內進行自注意力似乎更「原生」，但其二次方的計算成本使其在處理長序列時效率低下。TG的「外部記憶 + 交叉注意力」設計，有效地將複雜度分解為更可控的部分，這也體現了在保持 [[Borazjanizadeh-2025-008]] 中的端到端梯度流的同時，追求效率的平衡。
✍️ **Human**:



## 待解問題
在未來更高效的自注意力機制（如線性化注意力）出現後，上下文內記憶是否能與外部記憶在效率上競爭？或者說，兩種記憶方式是否存在結合的潛力，以同時獲得各自的優勢？
