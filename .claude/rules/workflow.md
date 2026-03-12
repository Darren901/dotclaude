# 工作流規範（Workflow Guidelines）

## 工具選型原則

| 工具                               | 優勢                                | 適用時機                    |
| ---------------------------------- | ----------------------------------- | --------------------------- |
| **Superpowers brainstorming**      | 設計探索、逐步釐清需求、架構選型    | 任何需要設計決策的任務      |
| **tdd-workflow + Superpowers TDD** | 測試規範 + Red-Green-Refactor 紀律  | 所有功能實作與 bug fix      |
| **Superpowers writing-plans**      | 展開單一複雜任務的執行步驟          | task 涉及多檔案連動或跨 session |
| **OpenSpec**                       | 輕量、token 友善、spec 生命週期追蹤 | 所有功能開發、spec 變更管理 |

---

## 開發流程

使用 **Superpowers brainstorming + OpenSpec + TDD 紀律**，適用所有任務（新功能或既有系統修改）：

```
[影響分析] 列出受影響的檔案、模組、下游依賴
  → brainstorming（設計探索、釐清需求與架構約束）
    → [設計複雜/需留存] superpowers 產出 design.md → opsx:propose（基於 design.md）
    → [設計簡單/上下文充足] opsx:propose（直接用當前 context）
      → [選擇性] writing-plans 展開 tasks.md 中的複雜任務（見下方說明）
        → opsx:apply + test-driven-development（每個 task 先測試再實作）
          → verification-before-completion（必須包含回歸測試）
            → opsx:archive（歸檔並同步 delta specs）
```

### 複雜任務展開（選擇性）

tasks.md 的任務粒度為高階（如「實作 XxxService」），遇到以下情況時可對單一任務使用 `writing-plans` 展開：

- 任務涉及多個檔案的連動修改
- 實作模式尚未在 codebase 中建立
- 需要跨 session 執行且不希望重新讀程式碼

`writing-plans` 的產出僅針對該任務，不需要對整個 change 規劃。
