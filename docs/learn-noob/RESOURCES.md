# ToolHive 学习资源

## Knowledge

- [ToolHive Architecture Overview](../arch/00-overview.md)
  项目维护者提供的总览，说明 CLI、workload、proxy、runtime 之间的关系。每次开始一条新调用链前先用它定位组件边界。
- [ToolHive Core Concepts](../arch/02-core-concepts.md)
  项目术语和接口位置索引，重点用于区分 workload、transport、proxy、RunConfig 和 permission profile。
- [ToolHive Workloads Lifecycle](../arch/08-workloads-lifecycle.md)
  用于后续深入 manager 的 deploy/stop/restart/delete 生命周期；Lesson 1 只取其中的运行入口。
- [Effective Go — Interfaces](https://go.dev/doc/effective_go)
  Go 官方文档；用于理解 ToolHive 中 `workloads.Manager`、`runtime.Deployer` 等接口如何隔离调用者与具体实现。
- [Go Concurrency Patterns: Context](https://go.dev/blog/context)
  Go 官方博客；用于理解 `context.Context` 如何把取消信号和请求边界沿调用链传递。
- [Cobra README](https://github.com/spf13/cobra)
  Cobra 官方仓库；用于理解 ToolHive 如何把命令、参数和 flags 组织成 CLI 调用入口。
- [Kubernetes Controllers](https://kubernetes.io/docs/concepts/architecture/controller/)
  Kubernetes 官方文档；后续从本地执行链切到 Operator 时，用来建立“期望状态 → 控制循环 → 实际状态”的基本模型。

## Wisdom (Communities)

- [ToolHive GitHub Discussions](https://github.com/stacklok/toolhive/discussions)
  适合在完成代码链路练习后，观察维护者和使用者如何讨论实际部署、兼容性与架构取舍。
- [Kubernetes Slack](https://slack.k8s.io/)
  后续开始学习 Operator 后再使用；当前不要求加入社区。

## Gaps

- 当前还没有为“ToolHive 版本与本地源码如何对应”建立固定阅读方法；后续会在第一轮课程中补上 commit/tag 记录。
