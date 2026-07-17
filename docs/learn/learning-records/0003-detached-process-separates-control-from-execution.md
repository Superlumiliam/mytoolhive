# Detached Process 分离一次性控制与长期执行

已纠正“`thv run` 父进程就是 Proxy”的理解：父进程负责解析参数、构造并保存 RunConfig、重新执行 `thv start <name> --foreground` 并记录 PID，随后退出；分离后的子进程才作为长期 workload supervisor 承载 Runner、Proxy、状态维护并拉起 MCP server 容器。这种设计让 workload 脱离终端持续运行，在不引入中央 daemon 的前提下获得按 workload 的故障、日志和生命周期隔离。

**Evidence:** 学习者先提出了父子进程假设，再追问这种设计的意义，已经把问题推进到前台进程、中央 daemon 与 detached supervisor 的架构取舍。
