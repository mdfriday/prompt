## **DDD 代码生成 原则**

### **目录结构**
代码应符合 **以下目录层级**，每一层都有明确的职责：
```
/cmd               # 入口层，初始化应用
/internal
  /application     # 应用层：业务用例、服务
  /domain          # 领域层：实体、工厂、值对象、仓储接口
  /interfaces      # 接口层：API、CLI、静态资源
/pkg               # 可复用的包
/vendor            # 依赖
```

**领域层（Domain） 结构**：
```
/internal/domain
  /{子领域}
    /entity        # 业务实体
    /factory       # 工厂模式创建对象
    /repository    # 仓储接口
    /type.go       # 类型定义
    /valueobject   # 值对象
```
  
---

### **代码生成原则**
生成代码时，遵循以下设计模式和原则：

## **1. 代码生成原则（Domain 层）**
#### **（1）实体（Entity）**
- **定义**：具有唯一标识符（ID）并拥有业务逻辑的对象。

#### **（2）聚合根（Aggregate Root）**
- **定义**：聚合（Aggregate）是一组相关对象，聚合根（Aggregate Root）是 **唯一允许外部访问的入口**，负责数据一致性。

#### **（3）值对象（Value Object）**
- **定义**：不可变对象，不具备唯一 ID，只包含业务逻辑，如 `Email`、`Address`。

#### **（4）仓储接口（Repository Interface）**
- **定义**：定义持久化方法，但不包含数据库实现。

#### **（5）工厂（Factory）**
- **定义**：封装对象创建逻辑，避免直接使用 `new`，确保符合业务规则。

### **生成代码的步骤**
1. **确定业务需求**
    - 识别核心业务对象（实体、值对象）。
    - 确定业务用例（增删改查、业务规则）。
2. **生成领域层（Domain）**
    - 定义 `entity`、`valueobject`、`repository`、`factory`。
3. **生成应用层（Application）**
    - 实现 `service`，调用 `repository`。
4. **生成接口层（Interfaces）**
    - 提供 HTTP API / CLI 入口。

### **6. 约束 & 规范**
✅ **日志**：使用 `"pkg/loggers"`，禁止 `fmt.Println`。  
✅ **错误处理**：使用 `errors.Wrap` 提供上下文。  
✅ **并发安全**：使用 `sync.Mutex` 或 `sync/atomic`。  
✅ **依赖管理**：使用 `wire` 进行依赖注入。
