# google_mcp_metadata

Claude Code 连 Google Workspace 官方远程 MCP（Gmail / Calendar）时用的 OAuth 授权服务器元数据。

为什么需要：Google 只有在授权请求带 `access_type=offline` 时才发 refresh token，Claude Code 没有配置项可加这个参数，所以登录约 1 小时就失效。这里的 `google-offline.json` 是 Google 公开的 `https://accounts.google.com/.well-known/openid-configuration` 原样复制，只把 `authorization_endpoint` 改成带 `?access_type=offline&prompt=consent`。在 `.mcp.json` 的 `oauth.authServerMetadataUrl` 指向本文件的 raw 地址即可。

文件里只有 Google 的公开地址，没有任何密钥、客户端 ID 或账号信息。

Google 的元数据如果变了（端点改名等），从上面的地址重新复制一份，再改 `authorization_endpoint` 这一行。
