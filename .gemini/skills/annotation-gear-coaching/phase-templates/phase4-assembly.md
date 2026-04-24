# Phase 4: Gear Assembly 輸出模板

## Connection Gear 草稿 - @{citekey}

### Frontmatter 更新

```yaml
geared: ["🔗TargetConnection"]
gear_status: draft  # → complete 當完成審閱
```

---

### Connection Gear⚙️

[English summary paragraph - 整合 Phase 3 深化後的洞見]

**Core thesis**: [Main finding/theory with [[cards/{citekey}-XXX]] links]

**Key findings**:
1. [Finding 1] - supported by [[cards/{citekey}-001|evidence]]
2. [Finding 2] - demonstrated in [[cards/{citekey}-007|experiment]]
3. [Finding 3] - theorized in [[cards/{citekey}-015|discussion]]

**Methodological contribution**: [If applicable, with card links]

**Key cards**:
- [[cards/{citekey}-001|description]]
- [[cards/{citekey}-007|description]]
- [[cards/{citekey}-015|description]]

**Theoretical connections**:
- Supports [[🔗Connection A]]: [how]
- Challenges [[🔗Connection B]]: [tension]
- Opens path to [[🤔Potential Thought]]

**Open questions from human review**:
1. [Question 1 from Phase 3 dialogue]
2. [Question 2]
3. [Question 3]

---

## AI 審閱檢查清單

- [ ] 核心洞見涵蓋關鍵卡片（Phase 1 標記的 🔑）
- [ ] 理論框架清晰（有明確的主張、證據、意涵）
- [ ] 潛在連結明確（指向具體 Connections）
- [ ] 待解問題具體可追蹤
- [ ] 句型符合 Gear Sentence Style（無 em-dash、無括弧清單、無關係子句、無從屬子句）
- [ ] Self-link 判斷：多篇論文並列引用時可用 `[[Author-Year|Name]]` 區分來源；單獨引用時改用純文字
- [ ] 無非英文範例：中文例句改用英文描述或刪除
- [ ] frontmatter `geared: true` 已更新

## 修訂建議（AI 提出）

- [建議 1]
- [建議 2]

---

**完成後**：
1. 更新 `gear_status: complete`
2. 通知 `connection-workflow-manager` 接手
3. 或使用 `/annotation-cross-link {citekey}` 識別更多連結
