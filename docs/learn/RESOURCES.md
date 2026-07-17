# ToolHive 企业级工具治理 Resources

## Knowledge

- [ToolHive Architecture Overview](../arch/00-overview.md)
  仓库内的平台边界与组件总览。用于建立 ToolHive 不只是容器启动器的心智模型。
- [Core Concepts](../arch/02-core-concepts.md)
  workload、transport、middleware、RunConfig、registry、group、vMCP 等统一术语的事实源。
- [Deployment Modes](../arch/01-deployment-modes.md)
  本地 CLI、API/UI 与 Kubernetes 模式的进程模型、状态位置和信任边界。
- [Workload Lifecycle](../arch/08-workloads-lifecycle.md)
  deploy、detached process、状态与生命周期的架构背景。用于建立全局顺序；具体执行先后应再用当前源码和测试校准。
- [Operator Architecture](../arch/09-operator-architecture.md)
  Kubernetes 控制面、CRD 分层、reconcile 与 Proxy Runner 职责的一手说明。用于核对 Operator 模式的权限和状态边界。
- [Architecture Reading Guide](../arch/README.md)
  当前架构文档索引。课程按治理闭环重新编排，但以这里的文档为一手依据。
- [`thv run` command](../../cmd/thv/app/run.go)
  本地 happy path 的命令入口。用于从输入解析进入 RunConfig、workload manager 和 runner。
- [`thv run` configuration assembly](../../cmd/thv/app/run_flags.go)
  registry/image 解析、flags 到 builder options、policy gate 与 image pull 的主路径。用于区分输入构建和执行阶段。
- [MCP server retriever](../../pkg/runner/retriever/retriever.go)
  registry lookup、raw image fallback、policy-before-pull 与协议镜像构建边界。用于定位镜像实际执行前的同步失败。
- [RunConfig builder](../../pkg/runner/config_builder.go)
  options 应用、环境变量、transport/port 默认值、校验和 schema version 的收敛边界。用于核对最终运行契约如何形成。
- [RunConfig contract](../../pkg/runner/config.go)
  共享 JSON/YAML wire format、有限的读取迁移、秘密引用与运行时字段边界。当前 schema version 是标记与默认值，不是通用兼容性校验门。
- [RunConfig state persistence](../../pkg/state/runconfig.go)
  本地 RunConfig 的保存与加载抽象。用于区分 codec、状态存储和运行时恢复职责。
- [Kubernetes manifest export](../../pkg/export/k8s.go)
  RunConfig 到 MCPServer 的字段映射。用于识别本地 JSON 与 Kubernetes 部署模型之间的有损转换。
- [Operator RunConfig rendering](../../cmd/thv-operator/controllers/mcpserver_runconfig.go)
  MCPServer CR 经 operator builder、额外校验与 ConfigMap 交付 RunConfig 的实现边界。
- [Workload manager](../../pkg/workloads/manager.go)
  生命周期管理接口及默认实现。用于理解运行、停止、删除、重启、状态和 detached process。
- [Local API server](../../cmd/thv/app/server.go)
  `thv serve` 的监听、Unix socket、认证和 server builder 入口。用于区分管理 API 与 MCP Proxy 流量边界。
- [API workload service](../../pkg/api/v1/workload_service.go)
  API 请求到 RunConfig、policy gate、状态保存和 detached workload 的转换路径。用于校准“API-managed”的真实含义。
- [MCPServer reconciler](../../cmd/thv-operator/controllers/mcpserver_controller.go)
  `MCPServer` 到 RunConfig ConfigMap、Proxy Deployment、Service 与 status 的收敛主线。用于学习声明式控制边界。
- [Kubernetes Proxy Runner](../../cmd/thv-proxyrunner/app/run.go)
  集群内 Proxy 如何读取 RunConfig、创建 Kubernetes runtime 并启动 Runner。用于连接 Operator 控制面与 server StatefulSet 执行面。
- [Runner](../../pkg/runner/runner.go)
  workload 执行与代理装配的核心实现。用于连接配置、runtime、transport 与 middleware。
- [Runtime setup](../../pkg/runtime/setup.go)
  RunConfig 如何转为 runtime deploy options、端口绑定和实际 workload。用于定位容器创建前后的失败边界。
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
