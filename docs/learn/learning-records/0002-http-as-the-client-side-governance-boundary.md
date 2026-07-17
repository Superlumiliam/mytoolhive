# HTTP 是 ToolHive 面向客户端的治理边界

已建立“北向连接”和“南向连接”的区分：MCP Client 通常通过 SSE 或 Streamable HTTP 访问 ToolHive Proxy，以便统一承载认证、授权、审计和遥测；Proxy 到 MCP server 的南向连接则取决于 server transport，可以是 HTTP 透明转发，也可以是 stdin/stdout 协议桥接。后续学习 transport 时应始终先标明连接位于 Proxy 的哪一侧，避免把 MCP server 的原生 transport 与 ToolHive 对外暴露的 transport 混为一谈。

**Evidence:** 学习者主动追问了 Client 与 Transparent Proxy 为什么采用 HTTP，并继续比较了 SSE 与 Streamable HTTP。
