---
name: annotation-cross-link
description: >
  識別論文與 vault 中其他 annotations、connections 的跨文獻連結機會，建立理論網絡。
  使用時機：Gear 完成後建立跨文獻連結、尋找相關研究、識別潛在 Connection 主題、擴展知識網絡。
  觸發詞：「找連結」「相關論文」「cross-link」「和哪些論文相關」「這篇論文連什麼」「跨文獻」「建立連結」。
  完成 Gear 後應主動建議使用此 skill，而非手動搜尋相關論文。
argument-hint: <citekey>
allowed-tools: Read, Glob, Grep, Bash
---

# Cross-Paper Linking

識別論文與 vault 中其他文獻的連結機會。

## 連結類型

| 類型 | 描述 | 標記 |
|------|------|------|
| **理論支持** | 支持相同理論框架 | 🤝 |
| **理論張力** | 挑戰或質疑對方觀點 | ⚡ |
| **方法互補** | 方法可相互借鑑 | 🔧 |
| **實證延伸** | 在對方基礎上擴展 | 📈 |

## 執行步驟

### Step 1: 掃描現有 Connections

```bash
Glob: ACT/1️⃣Conn/🔗*.md
```

識別可能相關的 Connection notes。

### Step 1.5: CLI 語意連結查詢

使用 Obsidian CLI 查詢已解析的連結圖（resolved link graph），取得檔案系統工具無法提供的語意連結資訊：

```bash
# 查詢目標 Annotation 的反向連結（哪些筆記連結到此論文）
obsidian vault=ACT_Base backlinks path="ACT/0️⃣Annotation/{Author-Year}/{Author-Year}.md" counts

# 查詢目標 Annotation 的連結密度（外向連結總數）
obsidian vault=ACT_Base links path="ACT/0️⃣Annotation/{Author-Year}/{Author-Year}.md" total
```

此步驟補充 Step 1 的 Glob 掃描：
- `backlinks counts` 回傳 Obsidian 實際解析的反向連結（含別名、嵌入），比 Grep `[[wikilink]]` 更準確
- 連結密度可快速判斷此論文在 vault 中的整合程度

### Step 2: 比對核心概念

從目標論文的 Connection Gear 提取：
- 核心論點
- 關鍵概念
- 理論框架

與現有 Connections 比對。

**CLI 輔助**：查詢目標論文的連結密度，評估整合程度：
```bash
obsidian vault=ACT_Base links path="ACT/0️⃣Annotation/{Author-Year}/{Author-Year}.md" total
```
連結密度低 → 優先建立跨文獻連結。

### Step 3: 掃描相關 Annotations

```bash
Glob: ACT/0️⃣Annotation/*/
Grep: [關鍵概念] in geared annotations
```

**CLI 輔助**：查詢每個相關 Connection 的反向連結，找出哪些 Annotations 已連結到該 Connection：
```bash
obsidian vault=ACT_Base backlinks path="ACT/1️⃣Conn/🔗{Connection Name}.md" counts
```
此資訊可識別尚未被納入 Connection 的 Annotations（連結機會）。

### Step 4: 生成連結報告

## 輸出格式

```markdown
## 跨論文連結報告 - @{citekey}

### 與現有 Connections 的關係

| Connection | 關係類型 | 說明 |
|------------|---------|------|
| [[🔗Mental Simulation]] | 🤝 理論支持 | 支持模擬理論的核心假設 |
| [[🔗Minimal Embodiment]] | ⚡ 理論張力 | 挑戰強具身認知觀點 |

### 相關 Annotations

| Annotation | 關係 | 潛在對話 |
|------------|------|---------|
| @Barsalou-1999 | 理論基礎 | PSS 理論的原始提出 |
| @Friedrich-2025 | 對立觀點 | 最小主義 vs 強具身 |

### 建議行動

1. 將此論文納入 [[🔗Mental Simulation]]
2. 考慮建立新 Connection: [[🔗xxx]]
3. 與 @Friedrich-2025 進行理論對話
```

## 下一步

連結識別後：
- **納入現有 Connection**：通知 `connection-workflow-manager`
- **建立新 Connection**：使用 `ALT + L` → Connection
- **深化對話**：回到 `/annotation-gear-coaching` Phase 3
