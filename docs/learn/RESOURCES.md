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
- [Transport architecture](../arch/03-transport-architecture.md)
  stdio 协议桥接、native HTTP 透明转发、remote proxy 与 session 的设计背景；细节以当前源码和协议测试校准。
- [Stdio transport](../../pkg/transport/stdio.go)
  容器 attach、HTTP-to-stdio message pump、proxy mode 与重连/监控边界。
- [HTTP transport](../../pkg/transport/http.go)
  本地 TargetURI 与 RemoteURL 到 transparent proxy 的收敛路径，以及 health、session 和 OAuth 注入边界。
- [Transparent proxy](../../pkg/transport/proxy/transparent/transparent_proxy.go)
  native HTTP server 的反向代理、session 跟踪、endpoint 重写、远端路径与 backend 路由实现。
- [Transport session manager](../../pkg/transport/session/manager.go)
  typed session、TTL 与本地/Redis storage 的生命周期抽象。
- [Middleware assembly](../../pkg/runner/middleware.go)
  typed RunConfig 字段到 middleware configs 的装配、相对顺序、入口防护与 backend egress 边界。
- [Middleware wiring in Runner](../../pkg/runner/runner.go)
  secret 解析、两条配置路径统一补全、factory 实例化及 transport 交付顺序。
- [Middleware integration tests](../../pkg/runner/webhook_integration_test.go)
  通过真实 handler chain 验证 mutating、validating、authz 与 backend 的执行次序。
- [Secrets Management](../arch/04-secrets-management.md)
  本地 provider 与 Kubernetes native Secret 两类交付架构的背景说明。
- [Secret providers](../../pkg/secrets/factory.go)
  provider 选择、system/user scope、capabilities 与 fallback 的事实入口。
- [Runtime deployment setup](../../pkg/runtime/setup.go)
  有效 permission profile、环境、network isolation、gateway 和 mount 意图进入 deployer 的边界。
- [Docker workload deployment](../../pkg/container/docker/client.go)
  本地容器 isolation、egress helper、mount 与 runtime 强制实现。
- [Registry architecture](../arch/06-registry-system.md)
  provider、metadata、remote/container server 与企业 registry 的设计背景。
- [Registry provider factory](../../pkg/registry/factory.go)
  API、remote JSON、local file、embedded provider 的选择、认证与缓存入口。
- [Server retriever and image verification](../../pkg/runner/retriever/retriever.go)
  名称解析、direct image fallback、provenance 验证、policy-before-pull 和执行物获取边界。
- [RunConfig create policy gate](../../pkg/runner/policy_gate.go)
  完整运行意图的 eager/runner 创建准入接口；默认实现允许全部。
- [File workload status manager](../../pkg/workloads/statuses/file_status.go)
  本地 status JSON、runtime、PID、proxy health 的合并与陈旧状态校准。
- [ToolHive process identity](../../pkg/process/toolhive_proxy.go)
  supervisor 进程发现、PID 验证与安全停止边界。
- [MCPServer controller](../../cmd/thv-operator/controllers/mcpserver_controller.go)
  finalizer、引用校验、RBAC、RunConfig、Proxy Deployment/Service 与 conditions 的一级收敛主线。
- [VirtualMCPServer watch graph](../../cmd/thv-operator/controllers/virtualmcpserver_watch_test.go)
  group/member/shared-config/composite/embedding 事件映射回引用方的可执行规格。
- [vMCP aggregator](../../pkg/vmcp/aggregator/default_aggregator.go)
  后端能力并发查询、工具冲突解析、广告视图与完整路由表的聚合边界。
- [vMCP core](../../pkg/vmcp/core/core_vmcp.go)
  identity、health、admission、composite tools 与按调用路由的统一领域入口。
- [vMCP incoming authentication](../../pkg/vmcp/auth/factory/incoming.go)
  OIDC/local/anonymous 认证、Identity 构造与 Cedar authorization 的入站边界。
- [vMCP session identity binding](../../pkg/vmcp/session/binding/binding.go)
  当前 `(iss, sub)` 会话所有者格式、匿名 sentinel 与“标识不等于凭证”的安全边界。
- [vMCP scalability limits](../arch/13-vmcp-scalability.md)
  每 Pod session cache、两类 TTL、Redis 热路径、状态恢复边界与 backend 故障模型的一手运维说明。
- [Operator replica controller tests](../../cmd/thv-operator/controllers/mcpserver_replicas_test.go)
  nil replicas、HPA hands-off、stdio cap、session storage warning 与 readyReplicas 的可执行规格。
- [vMCP session manager factory](../../pkg/vmcp/server/sessionmanager/factory.go)
  Pod-local LRU 容量、淘汰回调与 cache miss 处理的实现边界。
- [vMCP session restore factory](../../pkg/vmcp/session/factory.go)
  backend/session 恢复线索写入、`RestoreSession` 重连和工具路由重建的实现边界。
- [Observability architecture](../observability.md)
  ToolHive tracing、metrics、structured audit logging、middleware 顺序与 signal 配置的开发者说明。
- [Telemetry provider strategy](../../pkg/telemetry/providers/providers_strategy.go)
  no-op、OTLP tracing/metrics、Prometheus reader 及 unified MeterProvider 的实际选择逻辑。
- [Telemetry middleware and propagation](../../pkg/telemetry/middleware.go)
  HTTP/MCP spans、metrics、W3C context 提取与基于 HTTP status 的结果分类边界。
- [Audit event production](../../pkg/audit/auditor.go)
  主体/target/outcome、payload 保护和 HTTP 200 JSON-RPC application error 检测的事实入口。
- [MCPTelemetryConfig API](../../cmd/thv-operator/api/v1beta1/mcptelemetryconfig_types.go)
  共享配置、Secret-backed headers、CA bundle、per-workload serviceName 与 spec validation 契约。
- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/)
  MCP 官方规范。用于核对 transport、session、capability 与 JSON-RPC 语义，避免依赖二手解释。
- [Contributing guide](../../CONTRIBUTING.md)
  社区贡献、构建、测试与提交约定的一手依据。
- [Taskfile](../../Taskfile.yml)
  build、生成、lint、单元/集成/E2E 测试与文档更新的规范化入口。
- [Pull request checks](../../.github/workflows/run-on-pr.yml)
  spellcheck、license、lint、安全、测试、docs、codegen、charts、E2E 与 Operator CI 的仓库级证据图。

## Wisdom (Communities)

- [ToolHive GitHub repository](https://github.com/stacklok/toolhive)
  通过 issues、pull requests 和 review 观察真实设计取舍；用于挑选首个小贡献和验证提案。
- [Stacklok Discord](https://discord.gg/stacklok)
  与维护者和使用者核对真实需求、历史背景及隐含约束；提问前先附复现和已读代码路径。

## Gaps

- 首个实际贡献方向尚未确定；完成基础调用链课程后，从当前 issue 列表选择。
- 学习者对 Go、Kubernetes controller-runtime、OAuth/OIDC 的当前熟练度尚未通过练习验证。
