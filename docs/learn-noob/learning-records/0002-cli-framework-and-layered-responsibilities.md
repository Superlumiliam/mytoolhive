# CLI 框架与分层职责

已建立对 ToolHive CLI 分层的理解：Cobra 是命令行外壳，负责命令树、参数、flags、校验和路由；Viper 负责统一读取配置；pflag 是 flags 的底层解析库；slog/ToolHive logging 负责日志；context 与 signal 负责取消和进程生命周期；Bubble Tea/Lip Gloss 支持终端 UI。真正的 MCP Server 运行、workload 生命周期、transport、容器和 registry 等业务逻辑位于 `pkg/`，因此 ToolHive CLI 是“基于 Cobra 的入口层 + 对内部业务包的调用”，而不是把全部功能写在 Cobra 命令中。
