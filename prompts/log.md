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

### 5. **包含上下文信息（Context-Rich Logging）**
- 日志应携带 **关键上下文**，如请求 ID、用户 ID、IP 地址、会话信息等。
- 在微服务架构中，日志应能 **关联调用链**（Tracing），如 OpenTelemetry、Jaeger。

### 6. **避免敏感信息泄露（Security & Compliance）**
- **不得记录** 用户密码、银行卡号、API Token、私钥等敏感信息。
- **遵守法规**（如 GDPR、CCPA），用户相关日志应具备匿名化处理能力。

### 7. **可测试 & 可维护（Testable & Maintainable）**
- 日志格式应易于解析，方便 **自动化分析和告警系统** 处理。
- 使用 **日志轮转（Log Rotation）**，防止日志无限增长占满磁盘。
- 设定 **日志保留策略**（如保留 7 天），定期归档或清理。

**示例日志（JSON 格式）**：
```json
{
  "timestamp": "2025-02-22T12:34:56Z",
  "level": "ERROR",
  "service": "payment-gateway",
  "message": "Payment processing failed",
  "user_id": "123456",
  "request_id": "abc-def-789",
  "error_code": "PAYMENT_500",
  "stack_trace": "File 'payment.py', line 42, in process_payment"
}
```

### **总结**
高质量的日志应 **结构化、具备上下文、易于分析、符合安全规范**，并且支持可观测性，以便快速定位和解决问题。