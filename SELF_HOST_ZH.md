# 私有化部署 Firecrawl (Self-hosting Firecrawl)

#### 想要贡献代码？

欢迎来到 [Firecrawl](https://firecrawl.dev) 🔥！以下是将项目部署到本地的一些说明，以便您可以在自己的环境中运行并为其做出贡献。

如果您想参与贡献，请注意流程与其他开源仓库类似，即：Fork Firecrawl -> 修改代码 -> 运行测试 -> 提交 PR。

如果您有任何问题或需要帮助以便快速上手，请加入我们的 Discord 社区 [这里](https://discord.gg/gSmWdAkdwd) 获取更多信息，或在 Github 上提交 Issue [这里](https://github.com/firecrawl/firecrawl/issues/new/choose)！

## 为什么选择私有化部署？

对于那些拥有严格安全策略、要求数据必须保留在受控环境中的组织来说，私有化部署 Firecrawl 尤为有益。以下是考虑私有化部署的一些关键理由：

- **增强的安全性和合规性：** 通过私有化部署，您可以确保所有数据处理都符合内部和外部法规，将敏感信息保留在您的安全基础设施内。请注意，Firecrawl 是 Mendable 的产品，依赖 SOC2 Type2 认证，这意味着该平台在管理数据安全方面遵守高行业标准。
- **可定制的服务：** 私有化部署允许您根据特定需求定制服务（例如 Playwright 服务），或处理标准云服务可能不支持的特定用例。
- **学习和社区贡献：** 通过设置和维护您自己的实例，您可以更深入地了解 Firecrawl 的工作原理，这也能促进对项目做出更有意义的贡献。

### 注意事项

然而，也有一些限制和额外的责任需要注意：

1. **无法访问 Fire-engine：** 目前，Firecrawl 的私有化实例无法访问 Fire-engine，后者包含了用于处理 IP 封禁、机器人检测机制等高级功能。这意味着虽然您可以管理基本的爬取任务，但更复杂的场景可能需要额外的配置，或者可能不受支持。
2. **需要手动配置：** 如果您需要使用基本 fetch 和 Playwright 选项之外的爬取方法，则需要在 `.env` 文件中手动配置这些选项。这需要对技术有更深入的了解，并且可能涉及更多的设置时间。

私有化部署 Firecrawl 非常适合那些需要完全控制其爬取和数据处理环境的用户，但代价是需要额外的维护和配置工作。

## 部署步骤

1. 首先，安装依赖

- Docker [安装指南](https://docs.docker.com/get-docker/)


2. 设置环境变量

在根目录下创建一个 `.env` 文件，使用以下模板。

`.env:`
```
# ===== 必需的环境变量 ======
PORT=3002
HOST=0.0.0.0

# 注意：PORT 同时被主 API 服务器和 worker 存活检查端点使用

# 若要开启数据库验证，需要设置 Supabase。
USE_DB_AUTHENTICATION=false

# ===== 可选的环境变量 ======

## === AI 功能 (scrape 时的 JSON 格式, /extract API) ===
# 在此提供您的 OpenAI API 密钥以启用 AI 功能
# OPENAI_API_KEY=

# 实验性功能：使用 Ollama
# OLLAMA_BASE_URL=http://localhost:11434/api
# MODEL_NAME=deepseek-r1:7b
# MODEL_EMBEDDING_NAME=nomic-embed-text

# 实验性功能：使用任何兼容 OpenAI 的 API
# OPENAI_BASE_URL=https://example.com/v1
# OPENAI_API_KEY=

## === 代理 (Proxy) ===
# PROXY_SERVER 可以是完整 URL (如 http://0.1.2.3:1234) 或仅 IP 和端口组合 (如 0.1.2.3:1234)
# 如果您的代理无需验证，请勿取消注释 PROXY_USERNAME 和 PROXY_PASSWORD
# PROXY_SERVER=
# PROXY_USERNAME=
# PROXY_PASSWORD=

## === /search API ===
# 默认情况下，/search API 将使用 Google 搜索。

# 如果您想使用 SearXNG 服务器及其 JSON 格式替代直接使用 Google，可以在此指定。
# 您也可以自定义引擎和类别参数，但默认设置通常也能正常工作。
# SEARXNG_ENDPOINT=http://your.searxng.server
# SEARXNG_ENGINES=
# SEARXNG_CATEGORIES=

## === 其他 ===

# Supabase 设置 (用于支持数据库验证、高级日志记录等)
# SUPABASE_ANON_TOKEN=
# SUPABASE_URL=
# SUPABASE_SERVICE_TOKEN=

# 如果已设置验证并想用真实 API 密钥进行测试，请使用此项
# TEST_API_KEY=

# 此密钥允许您访问队列管理面板。如果您的部署是公网可访问的，请务必更改此项。
BULL_AUTH_KEY=CHANGEME

# 这现在由 docker-compose.yaml 自动配置。您应该不需要手动设置。
# PLAYWRIGHT_MICROSERVICE_URL=http://playwright-service:3000/scrape
# REDIS_URL=redis://redis:6379
# REDIS_RATE_LIMIT_URL=redis://redis:6379

## === PostgreSQL 数据库配置 ===
# 配置 PostgreSQL 凭据。这些应与 nuq-postgres 容器使用的凭据匹配。
# 如果更改这些设置，请确保三者保持一致。
# POSTGRES_USER=firecrawl
# POSTGRES_PASSWORD=firecrawl_password
# POSTGRES_DB=firecrawl

# 如果您有想要用于解析 PDF 的 llamaparse 密钥，请在此设置
# LLAMAPARSE_API_KEY=

# 如果您想发送服务器健康状态消息到 Slack，请在此设置
# SLACK_WEBHOOK_URL=

## === 系统资源配置 ===
# 最大 CPU 使用率阈值 (0.0-1.0)。当 CPU 使用率超过此值时，Worker 将拒绝新任务。
# 默认值: 0.8 (80%)
# MAX_CPU=0.8

# 最大 RAM 使用率阈值 (0.0-1.0)。当内存使用率超过此值时，Worker 将拒绝新任务。
# 默认值: 0.8 (80%)
# MAX_RAM=0.8

# 如果您想允许向自托管实例发送本地 webhook，请设置此项
# ALLOW_LOCAL_WEBHOOKS=true
```

### 安全注意事项

- **使用强 PostgreSQL 凭据。** `.env` 模板中的默认值仅供本地开发使用。部署到服务器时，请将 `POSTGRES_USER`、`POSTGRES_PASSWORD` 和 `POSTGRES_DB` 设置为安全值，并确保它们与数据库服务配置匹配。
- **保持数据库端口内部访问。** 提供的 `docker-compose.yaml` 不会将 PostgreSQL 暴露给宿主机或互联网。除非您使用防火墙限制访问，否则避免为 `nuq-postgres` 添加 `ports` 映射。要进行数据库维护，建议使用 `docker compose exec nuq-postgres psql` 或临时的、受防火墙保护的隧道。
- **保护管理界面。** 将 `BULL_AUTH_KEY` 设置为一个强密码，尤其是在任何可从不受信任网络访问的部署中。

3.  构建并运行 Docker 容器：

    ```bash
    docker compose build
    docker compose up
    ```

    如果遇到错误，请确保您使用的是 `docker compose` 而不是 `docker-compose`。
    
    这将运行一个本地 Firecrawl 实例，可通过 `http://localhost:3002` 访问。
    
    您应该可以在 `http://localhost:3002/admin/CHANGEME/queues` 看到 Bull 队列管理器界面。

5. (可选) 测试 API

如果您想测试 crawl 端点，可以运行以下命令：

  ```bash
  curl -X POST http://localhost:3002/v1/crawl \
      -H 'Content-Type: application/json' \
      -d '{
        "url": "https://firecrawl.dev"
      }'
  ```   

## 故障排除

本节提供了在设置或运行 Firecrawl 私有化实例时可能遇到的常见问题的解决方案。

### SDK 使用中的 API 密钥

**注意：** 在私有化实例中使用 Firecrawl SDK 时，API 密钥是可选的。仅在连接云服务 (api.firecrawl.dev) 时才需要 API 密钥。

### Supabase 客户端未配置 (Supabase client is not configured)

**症状：**
```bash
[YYYY-MM-DDTHH:MM:SS.SSSz]ERROR - Attempted to access Supabase client when it's not configured.
[YYYY-MM-DDTHH:MM:SS.SSSz]ERROR - Error inserting scrape event: Error: Supabase client is not configured.
```

**解释：**
此错误发生是因为 Supabase 客户端设置未完成。您应该仍能正常进行 scrape 和 crawl 操作。目前，私有化实例尚不支持配置 Supabase。

### 您正在绕过身份验证 (You're bypassing authentication)

**症状：**
```bash
[YYYY-MM-DDTHH:MM:SS.SSSz]WARN - You're bypassing authentication
```

**解释：**
此错误发生是因为 Supabase 客户端设置未完成。您应该仍能正常进行 scrape 和 crawl 操作。目前，私有化实例尚不支持配置 Supabase。

### Docker 容器启动失败

**症状：**
Docker 容器意外退出或无法启动。

**解决方案：**
使用以下命令检查 Docker 日志以获取错误信息：
```bash
docker logs [container_name]
```

- 确保 `.env` 文件中已正确设置所有必需的环境变量。
- 验证 `docker-compose.yml` 中定义的所有 Docker 服务配置正确，且所需镜像可用。

### Redis 连接问题

**症状：**
与 Redis 连接相关的错误，例如超时或“连接被拒绝”。

**解决方案：**
- 确保 Redis 服务在您的 Docker 环境中已启动并运行。
- 验证 `.env` 文件中的 `REDIS_URL` 和 `REDIS_RATE_LIMIT_URL` 指向正确的 Redis 实例，并确保它与 `docker-compose.yaml` 文件中的 URL (`redis://redis:6379`) 一致。
- 检查可能阻止 Redis 端口连接的网络设置和防火墙规则。

### API 端点无响应

**症状：**
对 Firecrawl 实例的 API 请求超时或无响应。

**解决方案：**
- 检查 Docker 容器状态，确保 Firecrawl 服务正在运行。
- 验证 `.env` 文件中的 `PORT` 和 `HOST` 设置正确，且没有其他服务占用相同端口。
- 检查网络配置，确保从发起 API 请求的客户端可以访问主机。

通过解决这些常见问题，您可以确保 Firecrawl 私有化实例的设置和运行更加顺畅。

## 在 Kubernetes 集群上安装 Firecrawl (简易版)

阅读 [examples/kubernetes/cluster-install/README.md](https://github.com/firecrawl/firecrawl/blob/main/examples/kubernetes/cluster-install/README.md) 获取有关如何在 Kubernetes 集群上安装 Firecrawl 的说明。

## 使用 Helm 在 Kubernetes 集群上安装 Firecrawl

阅读 [examples/kubernetes/firecrawl-helm/README.md](https://github.com/firecrawl/firecrawl/blob/main/examples/kubernetes/firecrawl-helm/README.md) 获取有关如何使用 Helm 在 Kubernetes 集群上安装 Firecrawl 的说明。
