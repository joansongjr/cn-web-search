---
name: cn-web-search
version: 0.2.0
description: 中文网页搜索 - 聚合 360 搜索 + DuckDuckGo + Hacker News + Reddit + ArXiv，无需 API Key
author: joansongjr
author_url: https://github.com/joansongjr
repository: https://github.com/joansongjr/cn-web-search
license: MIT
tags:
  - search
  - chinese
  - web-search
  - 360-search
  - duckduckgo
  - hacker-news
  - reddit
  - arxiv
  - no-api-key
  - free
  - 中文搜索
  - 学术搜索
---

# 中文网页搜索 (CN Web Search)

多引擎聚合搜索，零配置，无需 API Key。自动根据查询类型选择最适合的搜索引擎。

## 搜索引擎选择策略

| 查询类型 | 搜索引擎 | 原因 |
|---------|---------|------|
| **中文内容** | 360 搜索移动版 | 中文内容质量最好，无反爬 |
| **英文内容** | DuckDuckGo Lite | 纯 HTML，零反爬，Bing 索引 |
| **科技新闻/趋势** | Hacker News | 高质量科技讨论，AI/编程/Startup 必看 |
| **社区讨论** | Reddit | 全球最大社区，真实用户观点 |
| **学术论文** | ArXiv | 免费获取全球最新 AI/ML/物理等论文 |

---

## 1. 中文搜索：360 搜索

### 请求方式

```
web_fetch(url="https://m.so.com/s?q=QUERY", extractMode="text", maxChars=12000)
```

### 示例

```
web_fetch(url="https://m.so.com/s?q=英伟达最新财报", extractMode="text", maxChars=12000)
web_fetch(url="https://m.so.com/s?q=光模块行业趋势", extractMode="text", maxChars=12000)
```

### 解析结果

返回文本中搜索结果包含：
- **标题** — 独立行，带关键词高亮
- **摘要** — 1-3 行描述
- **来源和日期** — 如 "新浪财经 2025年11月20日"

提取前 5-10 条，跳过广告和推荐卡片。

---

## 2. 英文搜索：DuckDuckGo Lite

### 请求方式

```
web_fetch(url="https://lite.duckduckgo.com/lite/?q=QUERY", extractMode="text", maxChars=8000)
```

### 示例

```
web_fetch(url="https://lite.duckduckgo.com/lite/?q=NVIDIA+latest+earnings", extractMode="text", maxChars=8000)
web_fetch(url="https://lite.duckduckgo.com/lite/?q=AI+agents+2025", extractMode="text", maxChars=8000)
```

### 区域过滤

添加 `&kl=REGION`：
- `us-en` — 美国
- `uk-en` — 英国
- `hk-tzh` — 香港中文

---

## 3. 科技新闻：Hacker News（强烈推荐！）

### 请求方式

```
web_fetch(url="https://hn.algolia.com/api/v1/search?query=QUERY&tags=story&hitsPerPage=10", extractMode="text", maxChars=8000)
```

### 示例

```
web_fetch(url="https://hn.algolia.com/api/v1/search?query=OpenAI&tags=story&hitsPerPage=10", extractMode="text", maxChars=8000)
web_fetch(url="https://hn.algolia.com/api/v1/search?query=LLM+agent&tags=story&hitsPerPage=10", extractMode="text", maxChars=8000)
```

### 解析结果

返回 JSON 格式，结果在 `hits` 数组中。每条结果包含：
- `title` — 文章标题
- `url` — 原始链接
- `points` — 点赞数
- `author` — 作者
- `created_at` — 发布时间
- `num_comments` — 评论数

### 使用场景

- 搜最新 AI/科技趋势
- 找热门开源项目
- 了解程序员都在讨论什么
- "最近 Hacker News 上关于 LLM 的讨论"

---

## 4. 社区讨论：Reddit

### 请求方式

```
web_fetch(url="https://www.reddit.com/search.json?q=QUERY&limit=10", extractMode="text", maxChars=8000)
```

### 示例

```
web_fetch(url="https://www.reddit.com/search.json?q=Python+async&limit=10", extractMode="text", maxChars=8000)
web_fetch(url="https://www.reddit.com/search.json?q=machine+learning+tips&limit=10", extractMode="text", maxChars=8000)
```

### 解析结果

返回 JSON，结果在 `data.children[].data` 中。包含：
- `title` — 帖子标题
- `url` — 链接
- `score` —  upvotes
- `num_comments` — 评论数
- `subreddit` — 所属社区
- `selftext` — 正文（如果有）

### 使用场景

- 找真实用户的产品评价
- 搜教程、使用经验
- "Reddit 上关于 XXX 的讨论"

---

## 5. 学术论文：ArXiv

### 请求方式

```
web_fetch(url="http://export.arxiv.org/api/query?search_query=all:QUERY&max_results=5", extractMode="text", maxChars=5000)
```

### 示例

```
web_fetch(url="http://export.arxiv.org/api/query?search_query=all:large+language+model&max_results=5", extractMode="text", maxChars=5000)
web_fetch(url="http://export.arxiv.org/api/query?search_query=all:diffusion+model&max_results=5", extractMode="text", maxChars=5000)
```

### 解析结果

返回 XML 格式，每篇论文包含：
- `<title>` — 论文标题
- `<summary>` — 摘要
- `<author>` — 作者
- `<published>` — 发布日期
- `<id>` — 论文 ID（可用于下载 PDF）

### PDF 下载

论文 PDF 地址格式：
```
https://arxiv.org/pdf/{arxiv_id}.pdf
```

例如：`https://arxiv.org/pdf/2310.12345.pdf`

### 使用场景

- 搜最新学术论文
- 了解某技术领域的最新进展
- "最近有什么关于 XXX 的论文"

---

## 搜索策略建议

### 根据查询选择引擎

| 查询类型 | 推荐引擎 | 示例 |
|---------|---------|------|
| 中文资讯/新闻 | 360 搜索 | "光模块行业趋势"、"比亚迪最新消息" |
| 英文技术新闻 | Hacker News | "LLM 推理优化"、"AI agent 框架" |
| 产品评价/讨论 | Reddit | "iPhone 16 评测"、"Python 异步教程" |
| 学术研究 | ArXiv | "transformer 架构"、"扩散模型最新论文" |
| 通用英文搜索 | DDG Lite | "how to use OpenAI API" |

### 组合搜索策略

对于重要问题，可以组合多个引擎：

1. **全面调研**：360 搜索（中文）+ Hacker News（英文科技）
2. **产品选择**：Reddit（真实评价）+ DDG（技术规格）
3. **技术学习**：ArXiv（论文）+ Hacker News（社区讨论）

---

## 搜索-抓取模式 (Search → Fetch)

搜索只返回摘要。完整内容需要二次抓取：

1. **搜索** — 获取结果列表和 URLs
2. **筛选** — 挑出最相关的 2-3 个 URL
3. **抓取** — 用 `web_fetch(url="URL", extractMode="markdown")` 获取全文

### 示例

```
# 搜 Hacker News 上关于 AI agent 的讨论
web_fetch(url="https://hn.algolia.com/api/v1/search?query=AI+agent&tags=story&hitsPerPage=5", extractMode="text", maxChars=8000)

# 抓取排名第一的文章全文
web_fetch(url="https://example.com/article", extractMode="markdown", maxChars=20000)
```

---

## 不可用的搜索引擎

| 引擎 | 原因 |
|------|------|
| 百度 | 安全验证/验证码拦截 |
| Google | captcha 人机验证 |
| 搜狗 | 中文编码问题 |
| 头条搜索 | 需要 JS 渲染 |

---

## Tips

- 360 搜索：`maxChars=12000` → 约 8-10 条
- DDG：`maxChars=8000` → 约 10 条
- Hacker News：`hitsPerPage=10` → 最多 10 条
- Reddit：`limit=10` → 最多 10 条
- ArXiv：`max_results=5` → 最多 5 篇

### 搜索技巧

- 精确短语用引号：`q=%22深度学习%22`
- 加限定词：`Python 教程 2025`
- Hacker News 加 tags：`tags=story` 或 `tags=ask_hn`
- ArXiv 搜特定领域：`search_query=cat:cs.AI`（cs.AI 是 AI 分类）

---

## 局限性

- 无法按时间范围过滤（360/DDG）
- 纯文本结果，无图片/视频
- 偶发限速，等几秒重试
- Reddit 需要处理 JSON 解析
