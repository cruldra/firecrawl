# 自托管Firecrawl

#### 贡献者？

欢迎来到[Firecrawl](https://firecrawl.dev) 🔥！以下是一些关于如何在本地获取项目的说明，以便您可以在自己的环境中运行它并做出贡献。

如果您要贡献，请注意流程与其他开源仓库类似，即fork Firecrawl，进行更改，运行测试，提交PR。

如果您有任何问题或希望获得帮助，请加入我们的Discord社区[这里](https://discord.gg/gSmWdAkdwd)获取更多信息，或在Github[这里](https://github.com/firecrawl/firecrawl/issues/new/choose)提交issue！

## 为什么？

自托管Firecrawl对于具有严格安全政策、要求数据保留在受控环境中的组织特别有益。以下是考虑自托管的一些关键原因：

- **增强的安全性和合规性：** 通过自托管，您确保所有数据处理和处理都符合内部和外部法规，将敏感信息保留在您的安全基础设施内。请注意，Firecrawl是Mendable产品，依赖于SOC2 Type2认证，这意味着该平台遵循管理数据安全的高行业标准。
- **可定制的服务：** 自托管允许您定制服务，例如Playwright服务，以满足特定需求或处理标准云产品可能不支持的特定用例。
- **学习和社区贡献：** 通过设置和维护您自己的实例，您可以更深入地了解Firecrawl的工作原理，这也可以导致对项目更有意义的贡献。

### 注意事项

但是，需要注意一些限制和额外的责任：

1. **对Fire-engine的有限访问：** 目前，Firecrawl的自托管实例无法访问Fire-engine，其中包括处理IP阻止、机器人检测机制等的高级功能。这意味着虽然您可以管理基本的抓取任务，但更复杂的场景可能需要额外的配置或可能不受支持。
2. **需要手动配置：** 如果您需要使用超出基本fetch和Playwright选项的抓取方法，您需要在`.env`文件中手动配置这些。这需要对技术有更深入的了解，可能涉及更多的设置时间。

自托管Firecrawl对于那些需要完全控制其抓取和数据处理环境的人来说是理想的，但需要权衡额外的维护和配置工作。

## 步骤

1. 首先，开始安装依赖项

- Docker [说明](https://docs.docker.com/get-docker/)

2. 设置环境变量

使用下面的模板在根目录中创建一个`.env`文件。

`.env:`
```ini
# ===== 必需的环境变量 ======
PORT=3002
HOST=0.0.0.0

# 注意：PORT被主API服务器和worker活跃检查端点使用

# 要启用数据库身份验证，您需要设置Supabase。
USE_DB_AUTHENTICATION=false

# ===== 可选的环境变量 ======

## === AI功能（抓取时的JSON格式，/extract API）===
# 在此提供您的OpenAI API密钥以启用AI功能
# OPENAI_API_KEY=

# 实验性：使用Ollama
# OLLAMA_BASE_URL=http://localhost:11434/api
# MODEL_NAME=deepseek-r1:7b
# MODEL_EMBEDDING_NAME=nomic-embed-text

# 实验性：使用任何OpenAI兼容的API
# OPENAI_BASE_URL=https://example.com/v1
# OPENAI_API_KEY=

## === 代理 ===
# PROXY_SERVER可以是完整的URL（例如http://0.1.2.3:1234）或只是IP和端口组合（例如0.1.2.3:1234）
# 如果您的代理是未经身份验证的，请不要取消注释PROXY_USERNAME和PROXY_PASSWORD
# PROXY_SERVER=
# PROXY_USERNAME=
# PROXY_PASSWORD=

## === /search API ===
# 默认情况下，/search API将使用Google搜索。

# 如果您想使用SearXNG服务器而不是直接Google，可以指定启用JSON格式的SearXNG服务器。
# 您也可以自定义engines和categories参数，但默认值也应该工作得很好。
# SEARXNG_ENDPOINT=http://your.searxng.server
# SEARXNG_ENGINES=
# SEARXNG_CATEGORIES=

## === 其他 ===

# Supabase设置（用于支持数据库身份验证、高级日志记录等）
# SUPABASE_ANON_TOKEN=
# SUPABASE_URL=
# SUPABASE_SERVICE_TOKEN=

# 如果您已设置身份验证并想要使用真实API密钥进行测试，请使用此选项
# TEST_API_KEY=

# 此密钥让您访问队列管理面板。如果您的部署是公开可访问的，请更改此密钥。
BULL_AUTH_KEY=CHANGEME

# 这现在由docker-compose.yaml自动配置。您不需要设置它。
# PLAYWRIGHT_MICROSERVICE_URL=http://playwright-service:3000/scrape
# REDIS_URL=redis://redis:6379
# REDIS_RATE_LIMIT_URL=redis://redis:6379

# 如果您有想要用于解析pdf的llamaparse密钥，请设置
# LLAMAPARSE_API_KEY=

# 如果您想要向Slack发送服务器健康状态消息，请设置
# SLACK_WEBHOOK_URL=

# 如果您想要发送posthog事件如作业日志，请设置
# POSTHOG_API_KEY=
# POSTHOG_HOST=

## === 系统资源配置 ===
# 最大CPU使用阈值（0.0-1.0）。当CPU使用率超过此值时，Worker将拒绝新作业。
# 默认：0.8（80%）
# MAX_CPU=0.8

# 最大RAM使用阈值（0.0-1.0）。当内存使用率超过此值时，Worker将拒绝新作业。
# 默认：0.8（80%）
# MAX_RAM=0.8
```

3. 构建并运行Docker容器：
    
    ```bash
    docker compose build
    docker compose up
    ```

    如果遇到错误，请确保您使用的是`docker compose`而不是`docker-compose`。
    
    这将运行Firecrawl的本地实例，可以在`http://localhost:3002`访问。
    
    您应该能够在`http://localhost:3002/admin/CHANGEME/queues`看到Bull队列管理器UI。

5. *（可选）* 测试API

如果您想测试爬取端点，可以运行：

  ```bash
  curl -X POST http://localhost:3002/v1/crawl \
      -H 'Content-Type: application/json' \
      -d '{
        "url": "https://firecrawl.dev"
      }'
  ```   

## 故障排除

本节提供在设置或运行Firecrawl自托管实例时可能遇到的常见问题的解决方案。

### SDK使用的API密钥

**注意：** 在自托管实例中使用Firecrawl SDK时，API密钥是可选的。只有在连接到云服务（api.firecrawl.dev）时才需要API密钥。

### Supabase客户端未配置

**症状：**
```bash
[YYYY-MM-DDTHH:MM:SS.SSSz]ERROR - Attempted to access Supabase client when it's not configured.
[YYYY-MM-DDTHH:MM:SS.SSSz]ERROR - Error inserting scrape event: Error: Supabase client is not configured.
```

**解释：**
此错误发生是因为Supabase客户端设置未完成。您应该能够正常抓取和爬取。目前在自托管实例中无法配置Supabase。

### 您正在绕过身份验证

**症状：**
```bash
[YYYY-MM-DDTHH:MM:SS.SSSz]WARN - You're bypassing authentication
```

**解释：**
此错误发生是因为Supabase客户端设置未完成。您应该能够正常抓取和爬取。目前在自托管实例中无法配置Supabase。

### Docker容器启动失败

**症状：**
Docker容器意外退出或启动失败。

**解决方案：**
使用以下命令检查Docker日志中的任何错误消息：
```bash
docker logs [container_name]
```

- 确保在.env文件中正确设置了所有必需的环境变量。
- 验证docker-compose.yml中定义的所有Docker服务都正确配置，并且必要的镜像可用。

### Redis连接问题

**症状：**
与连接到Redis相关的错误，如超时或"连接被拒绝"。

**解决方案：**
- 确保Redis服务在您的Docker环境中正常运行。
- 验证.env文件中的REDIS_URL和REDIS_RATE_LIMIT_URL指向正确的Redis实例，确保它指向`docker-compose.yaml`文件中的相同URL（`redis://redis:6379`）
- 检查可能阻止连接到Redis端口的网络设置和防火墙规则。

### API端点无响应

**症状：**
对Firecrawl实例的API请求超时或无响应。

**解决方案：**
- 通过检查Docker容器状态确保Firecrawl服务正在运行。
- 验证.env文件中的PORT和HOST设置正确，并且没有其他服务使用相同端口。
- 检查网络配置以确保主机可以从发出API请求的客户端访问。

通过解决这些常见问题，您可以确保自托管Firecrawl实例的更顺畅设置和操作。

## 在Kubernetes集群上安装Firecrawl（简单版本）

阅读[examples/kubernetes/cluster-install/README.md](https://github.com/firecrawl/firecrawl/blob/main/examples/kubernetes/cluster-install/README.md)获取在Kubernetes集群上安装Firecrawl的说明。

## 使用Helm在Kubernetes集群上安装Firecrawl

阅读[examples/kubernetes/firecrawl-helm/README.md](https://github.com/firecrawl/firecrawl/blob/main/examples/kubernetes/firecrawl-helm/README.md)获取使用Helm在Kubernetes集群上安装Firecrawl的说明。
