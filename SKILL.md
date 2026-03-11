---
name: cn-web-search
version: 0.8.0
description: 中文网页搜索 - 聚合 14+ 搜索引擎，免费+付费混合，包含公众号文章搜索
author: joansongjr
author_url: https://github.com/joansongjr
repository: https://github.com/joansongjr/cn-web-search
license: MIT
tags:
  - search
  - chinese
  - wechat
  - 公众号
  - web-search
  - 360-search
  - sogou
  - bing
  - qwant
  - startpage
  - duckduckgo
  - hacker-news
  - reddit
  - arxiv
  - stackoverflow
  - github
  - caixin
  - wolfram
  - tavily
  - no-api-key
  - free
  - 中文搜索
  - 学术搜索
---

# 中文网页搜索 (CN Web Search)

多引擎聚合搜索，**免费+付费混合**。零配置，默认无需 API Key。

## 引擎分类

### 免费引擎（无需配置）

| 类别 | 引擎 | 说明 |
|------|------|------|
| 中文 | 360/搜狗/必应 | 主+备用 |
| 公众号 | 搜狗微信/必应索引 | ⭐ |
| 英文 | DDG/Qwant/Startpage/必应 | 主+备用 |
| 技术 | Stack Overflow/GitHub Trending | ⭐ |
| 专用 | Hacker News/Reddit/ArXiv | API |
| 投资 | 东方财富 | A股 |
| 深度 | 财新 | 财经 |
| 知识 | Wolfram Alpha | 计算 |

### 付费引擎（需要 API Key）

| 引擎 | 要求 | 说明 |
|------|------|------|
| **Tavily** | `TAVILY_API_KEY` | 免费 1000次/月 ⭐ |

---

## 1. Tavily 搜索（需要 API Key）

### 注册获取 Key

1. 访问 https://tavily.com 注册免费账号
2. 登录后进入 Dashboard，获取 API Key
3. 设置环境变量：`export TAVILY_API_KEY=你的Key`

### 使用方式

```
web_fetch(url="https://api.tavily.com/search?api_key=$TAVILY_API_KEY&q=QUERY", extractMode="text", maxChars=10000)
```

### 示例

```
web_fetch(url="https://api.tavily.com/search?api_key=$TAVILY_API_KEY&q=NVIDIA+earnings&max_results=10", extractMode="text", maxChars=10000)
```

### 特点

- **免费额度**：1000 次/月（足够个人使用）
- **结果质量高**：AI 优化的搜索结果
- **支持领域过滤**：include_domains、exclude_domains
- **适合**：需要高质量英文搜索结果时

---

## 2. 免费中文搜索

### 2.1 360 搜索（主）

```
https://m.so.com/s?q=QUERY
```

### 2.2 搜狗网页（备用1）

```
https://www.sogou.com/web?query=QUERY
```

### 2.3 必应中文（备用2）

```
https://cn.bing.com/search?q=QUERY
```

---

## 3. 免费英文搜索

### 3.1 DuckDuckGo Lite（主）

```
https://lite.duckduckgo.com/lite/?q=QUERY
```

### 3.2 Qwant

```
https://www.qwant.com/?q=QUERY&t=web
```

### 3.3 Startpage

```
https://www.startpage.com/do/search?q=QUERY&cluster=web
```

### 3.4 必应英文

```
https://www.bing.com/search?q=QUERY
```

---

## 4. 公众号搜索

### 4.1 搜狗微信

```
https://weixin.sogou.com/weixin?type=2&query=QUERY&page=1
```

### 4.2 必应公众号索引

```
https://cn.bing.com/search?q=site:mp.weixin.qq.com+QUERY
```

---

## 5. 技术/社区/学术

### 5.1 Hacker News

```
https://hn.algolia.com/api/v1/search?query=QUERY&tags=story&hitsPerPage=10
```

### 5.2 Reddit

```
https://www.reddit.com/search.json?q=QUERY&limit=10
```

### 5.3 ArXiv

```
http://export.arxiv.org/api/query?search_query=all:QUERY&max_results=5
```

### 5.4 Stack Overflow

```
https://stackoverflow.com/search?q=QUERY
```

### 5.5 GitHub Trending

```
https://github.com/trending?since=weekly
```

---

## 6. 其他专用

### 6.1 东方财富（投资）

```
https://search.eastmoney.com/search?keyword=QUERY
```

### 6.2 财新（深度报道）

```
https://search.caixin.com/search/?keyword=QUERY
```

### 6.3 Wolfram Alpha（知识问答）

```
https://www.wolframalpha.com/input?i=QUERY
```

---

## 使用示例

### 免费搜索

```
web_fetch(url="https://m.so.com/s?q=英伟达财报", extractMode="text", maxChars=12000)
web_fetch(url="https://lite.duckduckgo.com/lite/?q=AI+news", extractMode="text", maxChars=8000)
```

### Tavily 搜索（需要 Key）

```
# 先设置环境变量
export TAVILY_API_KEY=你的Key

# 然后调用
web_fetch(url="https://api.tavily.com/search?api_key=$TAVILY_API_KEY&q=semiconductor+industry&max_results=10", extractMode="text", maxChars=10000)
```

---

## 更新日志

### v0.8.0
- ✅ 增加 Tavily（付费引擎，需要 API Key，免费 1000次/月）

### v0.7.0
- ✅ 搜狗微信 + 必应公众号索引

### v0.6.0
- ✅ 财新 + Wolfram Alpha

### v0.5.0
- ✅ Stack Overflow + GitHub Trending + 东方财富

### v0.4.0
- ✅ Qwant + Startpage
