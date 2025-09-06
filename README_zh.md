<h3 align="center">
  <a name="readme-top"></a>
  <img
    src="https://raw.githubusercontent.com/firecrawl/firecrawl/main/img/firecrawl_logo.png"
    height="200"
  >
</h3>
<div align="center">
    <a href="https://github.com/firecrawl/firecrawl/blob/main/LICENSE">
  <img src="https://img.shields.io/github/license/firecrawl/firecrawl" alt="License">
</a>
    <a href="https://pepy.tech/project/firecrawl-py">
  <img src="https://static.pepy.tech/badge/firecrawl-py" alt="Downloads">
</a>
<a href="https://GitHub.com/firecrawl/firecrawl/graphs/contributors">
  <img src="https://img.shields.io/github/contributors/firecrawl/firecrawl.svg" alt="GitHub Contributors">
</a>
<a href="https://firecrawl.dev">
  <img src="https://img.shields.io/badge/Visit-firecrawl.dev-orange" alt="Visit firecrawl.dev">
</a>
</div>
<div>
  <p align="center">
    <a href="https://twitter.com/firecrawl_dev">
      <img src="https://img.shields.io/badge/Follow%20on%20X-000000?style=for-the-badge&logo=x&logoColor=white" alt="Follow on X" />
    </a>
    <a href="https://www.linkedin.com/company/104100957">
      <img src="https://img.shields.io/badge/Follow%20on%20LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="Follow on LinkedIn" />
    </a>
    <a href="https://discord.com/invite/gSmWdAkdwd">
      <img src="https://img.shields.io/badge/Join%20our%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Join our Discord" />
    </a>
  </p>
</div>

# 🔥 Firecrawl

为您的AI应用提供来自任何网站的清洁数据。具备先进的抓取、爬取和数据提取功能。

_此仓库正在开发中，我们仍在将自定义模块集成到单一仓库中。目前还未完全准备好用于自托管部署，但您可以在本地运行它。_

## 什么是Firecrawl？

[Firecrawl](https://firecrawl.dev?ref=github) 是一个API服务，它接收一个URL，爬取它，并将其转换为清洁的markdown或结构化数据。我们爬取所有可访问的子页面，并为每个页面提供清洁的数据。无需站点地图。查看我们的[文档](https://docs.firecrawl.dev)。

_嘿，加入我们的星标者吧 :)_

<a href="https://github.com/firecrawl/firecrawl">
  <img src="https://img.shields.io/github/stars/firecrawl/firecrawl.svg?style=social&label=Star&maxAge=2592000" alt="GitHub stars">
</a>

## 如何使用？

我们通过托管版本提供易于使用的API。您可以在[这里](https://firecrawl.dev/playground)找到演示和文档。如果您愿意，也可以自托管后端。

查看以下资源开始使用：
- [x] **API**: [文档](https://docs.firecrawl.dev/api-reference/introduction)
- [x] **SDK**: [Python](https://docs.firecrawl.dev/sdks/python), [Node](https://docs.firecrawl.dev/sdks/node)
- [x] **LLM框架**: [Langchain (python)](https://python.langchain.com/docs/integrations/document_loaders/firecrawl/), [Langchain (js)](https://js.langchain.com/docs/integrations/document_loaders/web_loaders/firecrawl), [Llama Index](https://docs.llamaindex.ai/en/latest/examples/data_connectors/WebPageDemo/#using-firecrawl-reader), [Crew.ai](https://docs.crewai.com/), [Composio](https://composio.dev/tools/firecrawl/all), [PraisonAI](https://docs.praison.ai/firecrawl/), [Superinterface](https://superinterface.ai/docs/assistants/functions/firecrawl), [Vectorize](https://docs.vectorize.io/integrations/source-connectors/firecrawl)
- [x] **低代码框架**: [Dify](https://dify.ai/blog/dify-ai-blog-integrated-with-firecrawl), [Langflow](https://docs.langflow.org/), [Flowise AI](https://docs.flowiseai.com/integrations/langchain/document-loaders/firecrawl), [Cargo](https://docs.getcargo.io/integration/firecrawl), [Pipedream](https://pipedream.com/apps/firecrawl/)
- [x] **社区SDK**: [Go](https://docs.firecrawl.dev/sdks/go), [Rust](https://docs.firecrawl.dev/sdks/rust)
- [x] **其他**: [Zapier](https://zapier.com/apps/firecrawl/integrations), [Pabbly Connect](https://www.pabbly.com/connect/integrations/firecrawl/)
- [ ] 想要SDK或集成？通过开启issue让我们知道。

要在本地运行，请参考[这里](https://github.com/firecrawl/firecrawl/blob/main/CONTRIBUTING.md)的指南。

### API密钥

要使用API，您需要在[Firecrawl](https://firecrawl.dev)上注册并获取API密钥。

### 功能特性

- [**抓取**](#抓取): 抓取URL并获取LLM就绪格式的内容（markdown、通过[LLM提取](#llm提取-beta)的结构化数据、截图、html）
- [**爬取**](#爬取): 抓取网页的所有URL并返回LLM就绪格式的内容
- [**映射**](#映射): 输入网站并获取所有网站URL - 极快
- [**搜索**](#搜索): 搜索网络并从结果中获取完整内容
- [**提取**](#提取-beta): 使用AI从单页、多页或整个网站获取结构化数据

### 强大功能

- **LLM就绪格式**: markdown、结构化数据、截图、HTML、链接、元数据
- **处理困难任务**: 代理、反机器人机制、动态内容（js渲染）、输出解析、编排
- **可定制性**: 排除标签、使用自定义头部爬取认证墙后的内容、最大爬取深度等...
- **媒体解析**: pdf、docx、图片
- **可靠性优先**: 设计用于获取您需要的数据 - 无论多么困难
- **操作**: 在提取数据前点击、滚动、输入、等待等
- **批处理**: 使用新的异步端点同时抓取数千个URL
- **变更跟踪**: 监控和检测网站内容随时间的变化

您可以在我们的[文档](https://docs.firecrawl.dev)中找到Firecrawl的所有功能以及如何使用它们

### 爬取

用于爬取URL和所有可访问的子页面。这会提交一个爬取任务并返回任务ID以检查爬取状态。

```bash
curl -X POST https://api.firecrawl.dev/v2/crawl \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer fc-YOUR_API_KEY' \
    -d '{
      "url": "https://docs.firecrawl.dev",
      "limit": 10,
      "scrapeOptions": {
        "formats": ["markdown", "html"]
      }
    }'
```

返回爬取任务id和检查爬取状态的url。

```json
{
  "success": true,
  "id": "123-456-789",
  "url": "https://api.firecrawl.dev/v2/crawl/123-456-789"
}
```

### 检查爬取任务

用于检查爬取任务的状态并获取其结果。

```bash
curl -X GET https://api.firecrawl.dev/v2/crawl/123-456-789 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

```json
{
  "status": "completed",
  "total": 36,
  "creditsUsed": 36,
  "expiresAt": "2024-00-00T00:00:00.000Z",
  "data": [
    {
      "markdown": "[Firecrawl Docs home page![light logo](https://mintlify.s3-us-west-1.amazonaws.com/firecrawl/logo/light.svg)!...",
      "html": "<!DOCTYPE html><html lang=\"en\" class=\"js-focus-visible lg:[--scroll-mt:9.5rem]\" data-js-focus-visible=\"\">...",
      "metadata": {
        "title": "Build a 'Chat with website' using Groq Llama 3 | Firecrawl",
        "language": "en",
        "sourceURL": "https://docs.firecrawl.dev/learn/rag-llama3",
        "description": "Learn how to use Firecrawl, Groq Llama 3, and Langchain to build a 'Chat with your website' bot.",
        "ogLocaleAlternate": [],
        "statusCode": 200
      }
    }
  ]
}
```

### 抓取

用于抓取URL并获取指定格式的内容。

```bash
curl -X POST https://api.firecrawl.dev/v2/scrape \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer YOUR_API_KEY' \
    -d '{
      "url": "https://docs.firecrawl.dev",
      "formats" : ["markdown", "html"]
    }'
```

响应：

```json
{
  "success": true,
  "data": {
    "markdown": "Launch Week I is here! [See our Day 2 Release 🚀](https://www.firecrawl.dev/blog/launch-week-i-day-2-doubled-rate-limits)[💥 Get 2 months free...",
    "html": "<!DOCTYPE html><html lang=\"en\" class=\"light\" style=\"color-scheme: light;\"><body class=\"__variable_36bd41 __variable_d7dc5d font-inter ...",
    "metadata": {
      "title": "Home - Firecrawl",
      "description": "Firecrawl crawls and converts any website into clean markdown.",
      "language": "en",
      "keywords": "Firecrawl,Markdown,Data,Mendable,Langchain",
      "robots": "follow, index",
      "ogTitle": "Firecrawl",
      "ogDescription": "Turn any website into LLM-ready data.",
      "ogUrl": "https://www.firecrawl.dev/",
      "ogImage": "https://www.firecrawl.dev/og.png?123",
      "ogLocaleAlternate": [],
      "ogSiteName": "Firecrawl",
      "sourceURL": "https://firecrawl.dev",
      "statusCode": 200
    }
  }
}
```

### 映射

用于映射URL并获取网站的url。这会返回网站上存在的大多数链接。

```bash cURL
curl -X POST https://api.firecrawl.dev/v2/map \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer YOUR_API_KEY' \
    -d '{
      "url": "https://firecrawl.dev"
    }'
```

响应：

```json
{
  "success": true,
  "links": [
    { "url": "https://firecrawl.dev", "title": "Firecrawl", "description": "Firecrawl is a tool that allows you to crawl a website and get the data you need." },
    { "url": "https://www.firecrawl.dev/pricing", "title": "Firecrawl Pricing", "description": "Firecrawl Pricing" },
    { "url": "https://www.firecrawl.dev/blog", "title": "Firecrawl Blog", "description": "Firecrawl Blog" },
    { "url": "https://www.firecrawl.dev/playground", "title": "Firecrawl Playground", "description": "Firecrawl Playground" },
    { "url": "https://www.firecrawl.dev/smart-crawl", "title": "Firecrawl Smart Crawl", "description": "Firecrawl Smart Crawl" }
  ]
}
```

#### 带搜索的映射

带有`search`参数的映射允许您在网站内搜索特定的url。

```bash cURL
curl -X POST https://api.firecrawl.dev/v2/map \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer YOUR_API_KEY' \
    -d '{
      "url": "https://firecrawl.dev",
      "search": "docs"
    }'
```

响应将是从最相关到最不相关的有序列表。

```json
{
  "success": true,
  "links": [
    { "url": "https://docs.firecrawl.dev", "title": "Firecrawl Docs", "description": "Firecrawl Docs" },
    { "url": "https://docs.firecrawl.dev/sdks/python", "title": "Firecrawl Python SDK", "description": "Firecrawl Python SDK" },
    { "url": "https://docs.firecrawl.dev/learn/rag-llama3", "title": "Firecrawl RAG Llama 3", "description": "Firecrawl RAG Llama 3" }
  ]
}
```

### 搜索

搜索网络并从结果中获取完整内容

Firecrawl的搜索API允许您执行网络搜索，并可选择在一次操作中抓取搜索结果。

- 选择特定的输出格式（markdown、HTML、链接、截图）
- 使用可定制参数搜索网络（语言、国家等）
- 可选择以各种格式从搜索结果中检索内容
- 控制结果数量并设置超时

```bash
curl -X POST https://api.firecrawl.dev/v2/search \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer fc-YOUR_API_KEY" \
  -d '{
    "query": "what is firecrawl?",
    "limit": 5
  }'
```

#### 响应

```json
{
  "success": true,
  "data": [
    {
      "url": "https://firecrawl.dev",
      "title": "Firecrawl | Home Page",
      "description": "Turn websites into LLM-ready data with Firecrawl"
    },
    {
      "url": "https://docs.firecrawl.dev",
      "title": "Documentation | Firecrawl",
      "description": "Learn how to use Firecrawl in your own applications"
    }
  ]
}
```

#### 带内容抓取

```bash
curl -X POST https://api.firecrawl.dev/v2/search \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer fc-YOUR_API_KEY" \
  -d '{
    "query": "what is firecrawl?",
    "limit": 5,
    "scrapeOptions": {
      "formats": ["markdown", "links"]
    }
  }'
```

### 提取 (Beta)

使用提示和/或模式从整个网站获取结构化数据。

您可以从一个或多个URL提取结构化数据，包括通配符：

单页：
示例：https://firecrawl.dev/some-page

多页/完整域名
示例：https://firecrawl.dev/*

当您使用/*时，Firecrawl将自动爬取并解析它在该域中可以发现的所有URL，然后提取请求的数据。

```bash
curl -X POST https://api.firecrawl.dev/v2/extract \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer YOUR_API_KEY' \
    -d '{
      "urls": [
        "https://firecrawl.dev/*",
        "https://docs.firecrawl.dev/",
        "https://www.ycombinator.com/companies"
      ],
      "prompt": "Extract the company mission, whether it is open source, and whether it is in Y Combinator from the page.",
      "schema": {
        "type": "object",
        "properties": {
          "company_mission": {
            "type": "string"
          },
          "is_open_source": {
            "type": "boolean"
          },
          "is_in_yc": {
            "type": "boolean"
          }
        },
        "required": [
          "company_mission",
          "is_open_source",
          "is_in_yc"
        ]
      }
    }'
```

```json
{
  "success": true,
  "id": "44aa536d-f1cb-4706-ab87-ed0386685740",
  "urlTrace": []
}
```

如果您使用SDK，它会自动为您拉取响应：

```json
{
  "success": true,
  "data": {
    "company_mission": "Firecrawl is the easiest way to extract data from the web. Developers use us to reliably convert URLs into LLM-ready markdown or structured data with a single API call.",
    "supports_sso": false,
    "is_open_source": true,
    "is_in_yc": true
  }
}
```

### LLM提取 (Beta)

用于从抓取的页面提取结构化数据。

```bash
curl -X POST https://api.firecrawl.dev/v2/scrape \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -d '{
    "url": "https://www.mendable.ai/",
    "formats": [
      {
        "type": "json",
        "schema": {
          "type": "object",
          "properties": {
            "company_mission": { "type": "string" },
            "supports_sso": { "type": "boolean" },
            "is_open_source": { "type": "boolean" },
            "is_in_yc": { "type": "boolean" }
          }
        }
      }
    ]
  }'
```

```json
{
  "success": true,
  "data": {
    "content": "Raw Content",
    "metadata": {
      "title": "Mendable",
      "description": "Mendable allows you to easily build AI chat applications. Ingest, customize, then deploy with one line of code anywhere you want. Brought to you by SideGuide",
      "robots": "follow, index",
      "ogTitle": "Mendable",
      "ogDescription": "Mendable allows you to easily build AI chat applications. Ingest, customize, then deploy with one line of code anywhere you want. Brought to you by SideGuide",
      "ogUrl": "https://mendable.ai/",
      "ogImage": "https://mendable.ai/mendable_new_og1.png",
      "ogLocaleAlternate": [],
      "ogSiteName": "Mendable",
      "sourceURL": "https://mendable.ai/"
    },
    "json": {
      "company_mission": "Train a secure AI on your technical resources that answers customer and employee questions so your team doesn't have to",
      "supports_sso": true,
      "is_open_source": false,
      "is_in_yc": true
    }
  }
}
```

### 无模式提取 (新功能)

您现在可以通过仅向端点传递`prompt`来进行无模式提取。LLM选择数据的结构。

```bash
curl -X POST https://api.firecrawl.dev/v2/scrape \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer YOUR_API_KEY' \
    -d '{
      "url": "https://docs.firecrawl.dev/",
      "formats": [
        {
          "type": "json",
          "prompt": "Extract the company mission from the page."
        }
      ]
    }'
```

### 使用操作与页面交互 (仅限云端)

Firecrawl允许您在抓取内容之前对网页执行各种操作。这对于与动态内容交互、浏览页面或访问需要用户交互的内容特别有用。

以下是如何使用操作导航到google.com、搜索Firecrawl、点击第一个结果并截图的示例。

```bash
curl -X POST https://api.firecrawl.dev/v2/scrape \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer YOUR_API_KEY' \
    -d '{
        "url": "google.com",
        "formats": ["markdown"],
        "actions": [
            {"type": "wait", "milliseconds": 2000},
            {"type": "click", "selector": "textarea[title=\"Search\"]"},
            {"type": "wait", "milliseconds": 2000},
            {"type": "write", "text": "firecrawl"},
            {"type": "wait", "milliseconds": 2000},
            {"type": "press", "key": "ENTER"},
            {"type": "wait", "milliseconds": 3000},
            {"type": "click", "selector": "h3"},
            {"type": "wait", "milliseconds": 3000},
            {"type": "screenshot"}
        ]
    }'
```

### 批量抓取多个URL (新功能)

您现在可以同时批量抓取多个URL。它与/crawl端点的工作方式非常相似。它提交一个批量抓取任务并返回任务ID以检查批量抓取的状态。

```bash
curl -X POST https://api.firecrawl.dev/v2/batch/scrape \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer YOUR_API_KEY' \
    -d '{
      "urls": ["https://docs.firecrawl.dev", "https://docs.firecrawl.dev/sdks/overview"],
      "formats" : ["markdown", "html"]
    }'
```

## 使用Python SDK

### 安装Python SDK

```bash
pip install firecrawl-py
```

### 爬取网站

```python
from firecrawl import Firecrawl

firecrawl = Firecrawl(api_key="fc-YOUR_API_KEY")

# 抓取网站（返回Document）
doc = firecrawl.scrape(
    "https://firecrawl.dev",
    formats=["markdown", "html"],
)
print(doc.markdown)

# 爬取网站
response = firecrawl.crawl(
    "https://firecrawl.dev",
    limit=100,
    scrape_options={"formats": ["markdown", "html"]},
    poll_interval=30,
)
print(response)
```

### 从URL提取结构化数据

使用LLM提取，您可以轻松从任何URL提取结构化数据。我们支持pydantic模式以使其更容易使用。以下是使用方法：

```python
from pydantic import BaseModel, Field
from typing import List

class Article(BaseModel):
    title: str
    points: int
    by: str
    commentsURL: str

class TopArticles(BaseModel):
    top: List[Article] = Field(..., description="Top 5 stories")

# 使用Pydantic模式的JSON格式
doc = firecrawl.scrape(
    "https://news.ycombinator.com",
    formats=[{"type": "json", "schema": TopArticles}],
)
print(doc.json)
```

## 使用Node SDK

### 安装

要安装Firecrawl Node SDK，您可以使用npm：

```bash
npm install @mendable/firecrawl-js
```

### 使用

1. 从[firecrawl.dev](https://firecrawl.dev)获取API密钥
2. 将API密钥设置为名为`FIRECRAWL_API_KEY`的环境变量，或将其作为参数传递给`Firecrawl`类。

```js
import Firecrawl from '@mendable/firecrawl-js';

const firecrawl = new Firecrawl({ apiKey: 'fc-YOUR_API_KEY' });

// 抓取网站
const doc = await firecrawl.scrape('https://firecrawl.dev', {
  formats: ['markdown', 'html'],
});
console.log(doc);

// 爬取网站
const response = await firecrawl.crawl('https://firecrawl.dev', {
  limit: 100,
  scrapeOptions: { formats: ['markdown', 'html'] },
});
console.log(response);
```

### 从URL提取结构化数据

使用LLM提取，您可以轻松从任何URL提取结构化数据。我们支持zod模式以使其更容易使用。以下是使用方法：

```js
import Firecrawl from '@mendable/firecrawl-js';
import { z } from 'zod';

const firecrawl = new Firecrawl({ apiKey: 'fc-YOUR_API_KEY' });

// 定义要提取内容的模式
const schema = z.object({
  top: z
    .array(
      z.object({
        title: z.string(),
        points: z.number(),
        by: z.string(),
        commentsURL: z.string(),
      })
    )
    .length(5)
    .describe('Top 5 stories on Hacker News'),
});

// 使用直接支持Zod模式的v2提取API
const extractRes = await firecrawl.extract({
  urls: ['https://news.ycombinator.com'],
  schema,
  prompt: 'Extract the top 5 stories',
});

console.log(extractRes);
```

## 开源版本 vs 云端服务

Firecrawl是在AGPL-3.0许可证下可用的开源软件。

为了提供最好的产品，我们在开源产品的基础上提供Firecrawl的托管版本。云解决方案使我们能够持续创新并为所有用户维护高质量、可持续的服务。

Firecrawl云端服务可在[firecrawl.dev](https://firecrawl.dev)获得，并提供开源版本中不可用的一系列功能：

![开源版本 vs 云端服务](https://raw.githubusercontent.com/firecrawl/firecrawl/main/img/open-source-cloud.png)

## 贡献

我们欢迎贡献！请在提交拉取请求之前阅读我们的[贡献指南](CONTRIBUTING.md)。如果您想要自托管，请参考[自托管指南](SELF_HOST.md)。

_最终用户在使用Firecrawl进行抓取、搜索和爬取时，有责任尊重网站的政策。建议用户在启动任何抓取活动之前遵守适用的隐私政策和网站使用条款。默认情况下，Firecrawl在爬取时遵守网站robots.txt文件中指定的指令。通过使用Firecrawl，您明确同意遵守这些条件。_

## 贡献者

<a href="https://github.com/firecrawl/firecrawl/graphs/contributors">
  <img alt="contributors" src="https://contrib.rocks/image?repo=firecrawl/firecrawl"/>
</a>

## 许可证声明

该项目主要在GNU Affero通用公共许可证v3.0（AGPL-3.0）下许可，如本仓库根目录中的LICENSE文件所指定。但是，该项目的某些组件在MIT许可证下许可。有关详细信息，请参考这些特定目录中的LICENSE文件。

请注意：

- AGPL-3.0许可证适用于项目的所有部分，除非另有说明。
- SDK和一些UI组件在MIT许可证下许可。有关详细信息，请参考这些特定目录中的LICENSE文件。
- 在使用或贡献此项目时，请确保您遵守您正在使用的特定组件的适当许可证条款。

有关特定组件许可的更多详细信息，请参考相应目录中的LICENSE文件或联系项目维护者。

<p align="right" style="font-size: 14px; color: #555; margin-top: 20px;">
    <a href="#readme-top" style="text-decoration: none; color: #007bff; font-weight: bold;">
        ↑ 返回顶部 ↑
    </a>
</p>
