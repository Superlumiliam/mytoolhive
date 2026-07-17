# Workload 与 Proxy 的绑定是逻辑一对一

基础心智模型可以采用“一个普通 workload 对应一个独立 Proxy 运行单元”：本地 CLI 通常表现为一个 detached Proxy process 和一个 server container，配置、端口、PID、日志与故障相互隔离。但这不是永恒的物理进程基数——Kubernetes 中一个 Proxy Deployment 可以扩展为多个副本，vMCP 则能以一个聚合网关连接多个 backend。

**Evidence:** 学习者提出“以 workload 为 unit 是否意味着每个 MCP server 都绑定一个 proxy process”，将理解从组成关系推进到了逻辑基数和部署副本问题。
