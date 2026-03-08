# Code Style & Conventions (程式碼風格與規範)

## General

- **Line Length**: Soft limit 120 characters

## Naming Conventions

- **Classes/Interfaces**: PascalCase
  - Services: `*Service` (e.g., `UserService`)
  - Repositories: `*Repository` (e.g., `UserRepository`)
  - Controllers: `*Controller` (e.g., `UserController`)
  - DTOs: `*DTO` 或使用 Java Records
- **Methods/Variables**: camelCase (e.g., `findUserById`, `userName`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `MAX_RETRY_COUNT`)
- **Packages**: lowercase, no underscores (e.g., `com.example.service`)

## Spring Components

- **Profile 檔案命名**：`application.yml`（共同）、`application-dev.yml`、`application-test.yml`、`application-prod.yml`
- **Annotations**:
  - `@Service` - Business logic layer
  - `@Repository` - Data access layer
  - `@Controller` / `@RestController` - Presentation layer
  - `@Component` - Generic components
- **Dependency Injection**:
  - **推薦**: Constructor injection（更易測試，避免循環依賴）
  - 避免 field injection (`@Autowired` on fields) 除非有特殊原因
  - 對於多個依賴，可考慮使用 Lombok's `@RequiredArgsConstructor`

## DTOs and Value Objects

- **Java Records**: 強烈推薦用於不可變的 DTOs 和 Value Objects
- **Lombok**: 可用於需要可變性的 DTOs (`@Data`, `@Builder`)
- **Validation**: 使用 Bean Validation (`@Valid`, `@NotNull`, `@Size` 等)

## Error Handling

- **Custom Exceptions**: 為業務邏輯定義領域特定的例外
  - 繼承自 `RuntimeException` 或 `Exception`
  - 包含有意義的訊息和上下文
- **Global Exception Handling**:
  - 使用 `@ControllerAdvice` / `@RestControllerAdvice`
  - 返回統一的錯誤響應格式
- **Tool/Function Methods**:
  - 如果方法會被外部系統調用（如 AI Agent Tools），不要拋出例外
  - 使用 Result 模式返回成功/失敗狀態

## Logging

- **Logger**: 使用 Lombok `@Slf4j`（取代手動宣告 `LoggerFactory`）
- **Format**: `log.info(">>>>>[Category] Message with {} placeholder", value);`
- **Category 範例**: `[API]`, `[Service]`, `[DB]`, `[Cache]`
