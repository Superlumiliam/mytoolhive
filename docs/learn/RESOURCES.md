# ToolHive 企业级工具治理 Resources

## Knowledge

- [ToolHive Architecture Overview](../arch/00-overview.md)
  仓库内的平台边界与组件总览。用于建立 ToolHive 不只是容器启动器的心智模型。
- [Core Concepts](../arch/02-core-concepts.md)
  workload、transport、middleware、RunConfig、registry、group、vMCP 等统一术语的事实源。
- [Deployment Modes](../arch/01-deployment-modes.md)
  本地 CLI、API/UI 与 Kubernetes 模式的进程模型、状态位置和信任边界。
- [Architecture Reading Guide](../arch/README.md)
  当前架构文档索引。课程按治理闭环重新编排，但以这里的文档为一手依据。
- [`thv run` command](../../cmd/thv/app/run.go)
  本地 happy path 的命令入口。用于从输入解析进入 RunConfig、workload manager 和 runner。
- [Workload manager](../../pkg/workloads/manager.go)
  生命周期管理接口及默认实现。用于理解运行、停止、删除、重启、状态和 detached process。
- [Runner](../../pkg/runner/runner.go)
  workload 执行与代理装配的核心实现。用于连接配置、runtime、transport 与 middleware。
- [Transport factory](../../pkg/transport/factory.go)
  transport 选择边界。用于比较 stdio、SSE 与 streamable HTTP 的实现分流。
- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/)
  MCP 官方规范。用于核对 transport、session、capability 与 JSON-RPC 语义，避免依赖二手解释。
- [Contributing guide](../../CONTRIBUTING.md)
  社区贡献、构建、测试与提交约定的一手依据。

## Wisdom (Communities)

- [ToolHive GitHub repository](https://github.com/stacklok/toolhive)
  通过 issues、pull requests 和 review 观察真实设计取舍；用于挑选首个小贡献和验证提案。
- [Stacklok Discord](https://discord.gg/stacklok)
  与维护者和使用者核对真实需求、历史背景及隐含约束；提问前先附复现和已读代码路径。

## Gaps

- 首个实际贡献方向尚未确定；完成基础调用链课程后，从当前 issue 列表选择。
- 学习者对 Go、Kubernetes controller-runtime、OAuth/OIDC 的当前熟练度尚未通过练习验证。
