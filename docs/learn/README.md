# ToolHive 企业级工具治理课程

本课程面向已有 MCP 基础的研发工程师。主线不是“ToolHive 有哪些命令”，而是一个企业治理闭环：

> 发现与准入 → 可移植配置 → 隔离运行 → 流量与身份控制 → 可观测生命周期 → Kubernetes 声明式治理 → 聚合治理

## 使用方式

每节 lesson 是一个短小、自包含的 HTML 单元。先完成课内回忆题和小实验，再把结果告诉教师以获得反馈；只有真正展示出的理解才进入 `learning-records/`。`reference/` 是长期速查材料，`docs/arch/` 和源码始终是事实源。

## 基础课程：贡献者主干

| 优先级 | 课程 | 能力验收 | 主要代码走读 |
|---|---|---|---|
| B1 | 平台心智模型与治理闭环 | 能解释 ToolHive 为何不只是 container runner，并画出核心边界 | `cmd/thv/`、`pkg/runner/`、`pkg/workloads/`、`pkg/transport/` |
| B2 | 部署形态与信任边界 | 能比较本地 detached、API 与 Operator 模式的进程、状态和安全边界 | `cmd/thv/main.go`、`pkg/api/`、`cmd/thv-operator/`、`cmd/thv-proxyrunner/` |
| B3 | 一次 `thv run` 端到端 | 能从参数沿 happy path 定位到容器和代理启动，并找到失败处理测试 | `cmd/thv/app/run.go` → `pkg/runner/config_builder.go` → `pkg/workloads/manager.go` → `pkg/runner/runner.go` |
| B4 | RunConfig：控制面契约 | 能解释字段、校验、持久化、export/import 及跨部署形态复用 | `pkg/runner/config.go`、`config_builder.go`、`pkg/state/` |
| B5 | Transport 与 Proxy | 能判断何时透明转发、何时协议桥接，并解释 session/endpoint | `pkg/transport/factory.go`、`proxy/`、`session/` |
| B6 | Middleware 管线 | 能说明认证、授权、过滤、审计、遥测的顺序为何属于安全语义 | `pkg/runner/middleware.go`、`pkg/authz/`、`pkg/transport/middleware/` |
| B7 | 最小权限与秘密 | 能追踪权限和 secret 从配置到 runtime 的解析与执行边界 | `pkg/secrets/`、`pkg/networking/`、`pkg/runner/permissions.go` |
| B8 | Registry 与供应链准入 | 能区分“目录”与“企业策展/策略门”，追踪 provider 和 policy gate | `pkg/registry/factory.go`、`provider_*.go`、`policy_gate.go` |
| B9 | Workload 生命周期与状态 | 能解释 RunConfig、PID、status、container 状态分离及失败清理 | `pkg/workloads/manager.go`、`statuses/`、`pkg/process/` |
| B10 | Operator 最小治理主链 | 能从 CRD 走到 reconcile、proxy-runner、工作负载与 status condition | `api/`、operator controllers、`cmd/thv-proxyrunner/app/run.go` |
| B11 | 社区贡献工程方法 | 能复现、定位边界、做最小改动、用 `task` 验证并组织小 PR | 邻近单元测试、Taskfile、贡献规范 |

基础结业项目：选择一个范围清晰的问题，完成“复现 → 调用链定位 → 最小修复 → 测试 → 文档判断 → 可评审提交”的完整闭环。

## 高阶课程：复杂与扩展能力

| 优先级 | 课程 | 重点 |
|---|---|---|
| A1 | vMCP 聚合网关 | backend discovery、能力聚合、命名冲突、路由、session、双边认证 |
| A2 | Operator CRD 图谱 | cross-resource watch、共享引用、conditions、drift 与 reconciliation |
| A3 | OAuth/OIDC 企业认证链 | 动态注册、token exchange、upstream token swap、远端 MCP 认证 |
| A4 | 多副本与分布式状态 | Redis session/auth storage、亲和性、TTL、容量与故障模型 |
| A5 | 可观测性深入 | OTel provider strategy、传播、metrics、traces、audit 与 Operator 配置 |
| A6 | 动态策略与扩展 | webhook、Cedar authorizer、rate limiting 及顺序风险 |
| A7 | Remote、升级与迁移 | 远端 workload 状态机、verified pull、TOCTOU、配置迁移与回滚取舍 |
| A8 | 企业 Registry 部署 | MCPRegistry、per-registry isolation、RBAC、配置交付与状态 |
| A9 | Composite Tools 与优化器 | workflow composition、tool search、embedding、code mode 等复杂能力 |
| A10 | Groups、Skills、Plugins | 组织与扩展体验；重要但不在运行治理主链 |

高阶结业项目：评审并实现一个带集成测试的 Operator、认证授权或 vMCP 功能，明确其安全、状态和扩展性取舍。

## 当前课程

1. [ToolHive 是治理平台，而不只是容器启动器](lessons/0001-toolhive-as-a-governance-platform.html)
2. [部署形态改变的是控制权与信任边界](lessons/0002-deployment-modes-and-trust-boundaries.html)
3. [把一次 `thv run` 追到真正运行](lessons/0003-trace-thv-run-end-to-end.html)
4. [RunConfig 是控制面契约，而不是内存快照](lessons/0004-runconfig-as-control-plane-contract.html)
5. [Transport 决定 Proxy 是协议桥接还是 HTTP 转发](lessons/0005-transport-and-proxy-boundaries.html)
6. [Middleware 顺序就是安全语义](lessons/0006-middleware-order-is-security.html)
7. [最小权限是文件、网络、秘密与 runtime 的交集](lessons/0007-least-privilege-and-secrets.html)
8. [Registry 是目录，供应链准入是多道门](lessons/0008-registry-and-supply-chain-admission.html)
9. [Workload 状态是多层证据的对账结果](lessons/0009-workload-lifecycle-and-state.html)

## 长期速查

- [统一术语表](reference/toolhive-glossary.html)
- [治理闭环](reference/governance-loop.html)
- [代码库地图](reference/codebase-map.html)
- [部署形态与信任边界](reference/deployment-trust-boundaries.html)
- [`thv run` 调用链](reference/thv-run-call-chain.html)
- [RunConfig 控制面契约](reference/runconfig-contract.html)
- [Transport 与 Proxy 决策表](reference/transport-proxy-decision-table.html)
- [Middleware 顺序评审清单](reference/middleware-order-checklist.html)
- [最小权限与秘密审计清单](reference/least-privilege-audit.html)
- [Registry 与供应链准入清单](reference/registry-admission-checklist.html)
- [Workload 状态诊断表](reference/workload-state-diagnosis.html)
