# AI Agent Charter (AI 代理憲章)

## ⚠️ 關鍵指令

**必須使用繁體中文 (Traditional Chinese) 與使用者溝通。**

**實作任何功能或 Bug Fix 的強制順序（無例外）：**
1. 禁止在呼叫 `tdd-workflow` Skill 之前使用 Write 或 Edit 工具修改任何程式碼
2. 禁止在呼叫 `superpowers:test-driven-development` Skill 之前開始實作
3. 違反以上兩點視為流程錯誤，必須立即停止並重新執行正確順序

---

## 行為規範

**意圖判斷**
- 若使用者問題以「建議」、「分析」、「評估」、「怎麼做」開頭，只給文字建議，**禁止修改任何檔案**，除非使用者明確說「請實作」或「幫我改」
- 若不確定使用者意圖，先問清楚再動手

**使用既有程式碼**
- 實作前必須先 Grep/Glob 搜尋 codebase 是否已有對應的 utility、helper 或 pattern
- 找到既有實作就直接用，禁止重新造輪子

**建立新檔案前必須確認**
- 建立任何新檔案（包含 Skill 檔、config 檔）前，必須先明確告知使用者並等待確認
- 唯一例外：TDD 流程中寫測試檔，可直接進行

**誠實回答行為問題**
- 若使用者詢問「你是否真的遵守某規則」，直接說明實際行為，禁止給理想化答案

---

## 專案背景

**Project**: [專案名稱 - 請在此填入]
**Description**: [專案描述 - 請在此填入]
**開發模式**: [綠地 Greenfield / 褐地 Brownfield]

**Tech Stack**:

- Java 21（請根據專案調整）
- Spring Boot 3.x（請根據專案調整）
- Database: [PostgreSQL / MySQL / MS SQL 等]
- Cache: [Redis / Caffeine / None]
- Additional: [Spring AI / GraphQL / Kafka 等]

---

## 常用命令

```bash
mvn clean compile   # 編譯驗證
mvn test            # 執行測試
mvn spring-boot:run # 啟動應用程式
```

---

## 專案結構

```
src/main/java/com/example/
├── controller/      # REST API 入口
├── service/         # 業務邏輯
├── jpa/
│   ├── repository/  # 資料存取
│   └── entity/      # Entity / Value Object
├── dto/             # Request / Response DTOs
└── config/          # Spring 配置類
```

---

## 禁止事項

- 禁止 field injection（`@Autowired` on fields）
- 禁止 wildcard import（`import java.util.*`）
- 禁止將密碼、API keys、token 寫入程式碼或 log
- 禁止直接修改已發布的 Flyway migration 檔案（如使用 Flyway）
- 禁止在 Controller 直接操作 Entity，必須經過 DTO（如使用 JPA）

---

## 對話規範

### Understand（每次對話開始時）

對話開始先讀 `README.md`、`pom.xml`（或 `build.gradle`）、`application.yml` 確認專案背景。

### Communicate（每次完成後）

必須用**繁體中文**輸出：做了什麼（What）、為什麼這樣設計（Why）、需確認的問題（若有）、已知限制或後續建議（若有）。

