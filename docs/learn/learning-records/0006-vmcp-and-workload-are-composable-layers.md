# vMCP 与 Workload 是可组合的治理层级

已区分两者职责：Workload 管理单个 MCP 服务的运行、隔离、流量边界与生命周期，vMCP 管理多个 backend 的能力聚合、冲突处理、路由和统一入口；它们不是互斥的两种模式。二者可以独立部署、实现上相对解耦，也可以组合为“vMCP 聚合多个 ToolHive workloads”，而 vMCP backend 也可以是外部 MCP endpoint。

**Evidence:** 学习者主动检验“二者是否截然不同且相互独立”的假设，完成了从二选一模式到分层可组合架构的修正。
