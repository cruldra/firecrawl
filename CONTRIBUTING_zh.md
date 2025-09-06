# 贡献者指南：

欢迎来到[Firecrawl](https://firecrawl.dev) 🔥！以下是一些关于如何在本地获取项目的说明，以便您可以在自己的环境中运行它（并做出贡献）

如果您要贡献，请注意流程与其他开源仓库类似，即（fork firecrawl，进行更改，运行测试，提交PR）。如果您有任何问题，并希望获得帮助，请联系help@firecrawl.com获取更多信息或提交issue！

## 在本地运行项目

首先，开始安装依赖项：

1. node.js [说明](https://nodejs.org/en/learn/getting-started/how-to-install-nodejs)
2. pnpm [说明](https://pnpm.io/installation)
3. redis [说明](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/)

在/apps/api/目录中的.env文件中设置环境变量，您可以复制.env.example中的模板。

首先，我们不会设置身份验证或任何可选的子服务（pdf解析、JS阻止支持、AI功能）

.env:

```ini
# ===== 必需的环境变量 ======
NUM_WORKERS_PER_QUEUE=8
PORT=3002
HOST=0.0.0.0
REDIS_URL=redis://localhost:6379
REDIS_RATE_LIMIT_URL=redis://localhost:6379

## 要启用数据库身份验证，您需要设置supabase。
USE_DB_AUTHENTICATION=false

# ===== 可选的环境变量 ======

# Supabase设置（用于支持数据库身份验证、高级日志记录等）
SUPABASE_ANON_TOKEN=
SUPABASE_URL=
SUPABASE_SERVICE_TOKEN=

# 其他可选项
TEST_API_KEY= # 如果您已设置身份验证并想要使用真实API密钥进行测试，请使用此选项
OPENAI_API_KEY= # 为依赖LLM的功能添加（图像alt生成等）
BULL_AUTH_KEY= @
PLAYWRIGHT_MICROSERVICE_URL=  # 如果您想运行playwright回退，请设置
LLAMAPARSE_API_KEY= # 如果您有想要用于解析pdf的llamaparse密钥，请设置
SLACK_WEBHOOK_URL= # 如果您想要发送slack服务器健康状态消息，请设置
POSTHOG_API_KEY= # 如果您想要发送posthog事件如作业日志，请设置
POSTHOG_HOST= # 如果您想要发送posthog事件如作业日志，请设置
```

### 安装依赖项

首先，使用pnpm安装依赖项。

```bash
# cd apps/api # 确保您在正确的文件夹中
pnpm install # 确保您有pnpm版本9+！
```

### 运行项目

您需要打开3个终端。这里有一个[截至2024年10月准确的视频指南](https://youtu.be/LHqg5QNI4UY)。

### 终端1 - 设置redis

在项目内的任何地方运行命令

```bash
redis-server
```

### 终端2 - 设置workers

现在，导航到apps/api/目录并运行：

```bash
pnpm run workers
# 如果您要使用[llm-extract功能](https://github.com/firecrawl/firecrawl/pull/586/)，您还应该导出OPENAI_API_KEY=sk-______
```

这将启动负责处理爬取作业的workers。

### 终端3 - 设置主服务器

要做到这一点，导航到apps/api/目录并运行，如果您还没有安装pnpm，请在这里安装：https://pnpm.io/installation
接下来，使用以下命令运行您的服务器：

```bash
pnpm run start
```

### 终端3 - 发送我们的第一个请求

好的：现在让我们发送我们的第一个请求。

```curl
curl -X GET http://localhost:3002/test
```

这应该返回响应Hello, world!

如果您想测试爬取端点，可以运行：

```curl
curl -X POST http://localhost:3002/v1/crawl \
    -H 'Content-Type: application/json' \
    -d '{
      "url": "https://mendable.ai"
    }'
```

### 替代方案：使用Docker Compose

为了更简单的设置，您可以使用Docker Compose来运行所有服务：

1. 先决条件：确保您已安装Docker和Docker Compose
2. 将`.env.example`文件复制到`/apps/api/`目录中的`.env`并根据需要进行配置
3. 从根目录运行：

```bash
docker compose up
```

这将自动以正确的配置启动Redis、API服务器和workers。

## 测试：

最好的方法是使用`npm run test:local-no-auth`运行测试，如果您想在没有身份验证的情况下运行测试。

如果您想在有身份验证的情况下运行测试，请运行`npm run test:prod`
