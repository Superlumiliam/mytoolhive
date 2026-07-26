# Mission: 从代码调用链掌握 ToolHive 架构

## Why

通过沿真实功能的 DFS 调用链阅读 ToolHive，建立对 CLI、Go 分层设计、MCP 代理运行时和 Kubernetes Operator 的整体心智模型，能够在真实工作和面试中解释“一个 MCP Server 请求是怎样被创建、运行、代理和管理的”。

## Success looks like

- 能从一个 `thv` 命令入口，独立追踪到关键接口、实现和外部副作用。
- 能用 Go 的视角解释 ToolHive 为什么使用 `interface`、`context.Context`、配置对象和 manager/runner/runtime 分层。
- 能把本地运行链路迁移到 Kubernetes：区分 CLI 直接执行与 Controller 根据期望状态进行 reconcile。
- 面试时能画出一个功能的调用链，并说明每一层的职责、替换点和失败边界。

## Constraints

- Go 了解一些但不熟练；Kubernetes 基础为零；MCP 协议已有掌握。
- 偏好以一个功能从上到下贯通的 DFS 调用链学习，而不是先铺开全部概念。
- 每节课短小、只解决一个可验证的问题；通过回忆题和代码定位练习巩固长期记忆。
- 所有学习文件放在 `docs/learn-noob/`。

## Out of scope

- 第一阶段不追求一次性读完所有包、所有 CRD 或所有 middleware。
- 不先从 Kubernetes 入门，而是在本地调用链中遇到需要的抽象时再补 Kubernetes 知识。
