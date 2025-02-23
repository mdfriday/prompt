# **Logging Best Practices（打日志的最佳实践）**

## **适用于软件开发中的日志记录**

### 1. **清晰 & 结构化（Clear & Structured）**
- 日志应 **结构化**（JSON、Key-Value），方便检索和分析。
- **保持一致性**，不同模块的日志格式应统一，如 `[时间] [级别] [模块] [消息]`。

### 2. **面向可观测性（Observability-Oriented）**
- 记录 **关键业务流程** 的日志，以便追踪用户行为和系统状态。
- 在 **异常处理** 处写日志，确保可快速溯源问题。
- 结合 **Trace ID / Request ID**，确保分布式系统的可追踪性。

### 3. **遵循 5W1H 原则（Who, What, When, Where, Why, How）**
日志内容应包括：
- **Who** - 相关用户或系统组件（User ID, Service Name）
- **What** - 发生了什么（操作内容，事件类型）
- **When** - 事件发生的时间（时间戳，UTC 格式）
- **Where** - 代码位置（文件名、函数名、行号）
- **Why** - 事件的原因（错误详情、输入参数）
- **How** - 事件的执行方式（调用链、影响范围）

### 4. **合理选择日志级别（Log Levels）**
不同级别的日志适用于不同场景：
- **DEBUG** - 仅用于开发调试，不在生产环境启用。
- **INFO** - 记录关键业务流程，如 `用户登录成功`。
- **WARNING** - 记录可能的问题，如 `Redis 连接超时，已重试`。
- **ERROR** - 记录失败的操作，如 `数据库插入失败，错误码 500`。
- **FATAL** - 记录系统崩溃或不可恢复的错误，如 `服务启动失败，进程退出`。
