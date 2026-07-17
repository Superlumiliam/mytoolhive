# Workload 是逻辑治理单元而非容器边界

已明确 Workload 表示 ToolHive 管理的完整逻辑单元，涵盖 RunConfig、Proxy/transport/middleware、运行目标、状态、日志和生命周期，并不表示“被 container 包含的一切”。本地模式下 Proxy 通常运行在宿主机的 detached `thv` 进程中而 MCP server 位于容器内；Kubernetes 中 Proxy 和 server 分别位于 proxy-runner Deployment 与 server StatefulSet，remote workload 甚至可以没有本地 server container。

**Evidence:** 学习者通过连续追问 Proxy 是否位于 container，以及每个 MCP server 是否绑定 Proxy，主动澄清了逻辑包含、进程边界与部署边界。
