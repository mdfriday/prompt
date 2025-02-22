# **Code Generation Best Practices（代码生成最佳实践）**

## **适用于自动生成代码的场景**

### 1. **清晰 & 可维护（Readable & Maintainable）**
- **生成代码应易读**，符合标准的代码风格（如 PEP8、GoFmt、Prettier）。
- **变量、函数、类命名应清晰**，避免随机命名，如 `func_123()` 或 `tempVar`。
- 代码应 **可扩展**，避免硬编码（hardcoded values）。

### 2. **符合 SOLID 原则（SOLID Principles）**
生成的代码应遵循 **SOLID** 设计原则，以提高可维护性和可扩展性：
- **S（单一职责）**：每个类/函数只做一件事。
- **O（开闭原则）**：代码应易于扩展，避免直接修改。
- **L（里氏替换）**：子类应可替换父类，不影响功能。
- **I（接口隔离）**：避免强制实现不必要的方法。
- **D（依赖倒置）**：应依赖抽象（接口）而非具体实现。

### 3. **确保可测试性（Testable）**
- **代码应具备单元测试**（Unit Test），可自动化验证。
- 避免直接依赖外部系统（如数据库、API），应使用 **依赖注入（Dependency Injection）**。
- 代码逻辑应可拆解为小的测试单元，便于 **Mock 测试**。

### 4. **遵循代码标准（Coding Standards）**
- **风格统一** Golangci-lint。
- **结构清晰**，遵循最佳实践，DDD（Domain-Driven Design）。
- 代码应包含 **必要的注释**，但不过度。

### 5. **性能优化（Performance-Oriented）**
- **避免不必要的计算**，如重复循环、无效的数据库查询。
- **优先选择高效的数据结构**，如 `map` 代替 `list` 查找。
- **非阻塞设计**，如异步编程、缓存提升响应速度。

### 6. **代码安全（Security & Compliance）**
- **防止 SQL 注入**（使用 ORM、参数化查询）。
- **避免 Hardcoded Secrets**，应使用环境变量或密钥管理（如 Vault）。
- **遵守安全规范**（如 OWASP Top 10），避免 XSS、CSRF、RCE 攻击。

### 7. **模块化 & 复用（Modular & Reusable）**
- 代码应 **模块化**，避免大而全的函数。
- **重复代码应提取为通用函数或库**，提高复用性。
- 采用 **接口（Interface）+ 实现（Implementation）**，增强灵活性。
