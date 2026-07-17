# Streamable HTTP 演进了旧 HTTP+SSE 模型

已建立两者的核心差异：旧 HTTP+SSE transport 使用独立 SSE 下行端点和 POST 上行端点，并依赖长期 SSE 连接；Streamable HTTP 以单一 MCP endpoint 和 HTTP POST 为核心，可直接返回 JSON，也可按需返回 SSE stream，并用可选 GET stream 支持服务端主动消息。二者都传输 JSON-RPC 且可使用 SSE，但新实现应优先选择 Streamable HTTP，旧 SSE 主要承担兼容性角色。

**Evidence:** 学习者专门要求比较两种 transport 的异同，这为后续走读 ToolHive transparent proxy、session 与兼容分支建立了必要前提。
