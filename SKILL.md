---
name: cn-web-search
version: 0.4.0
description: 中文网页搜索 - 聚合 360 + 搜狗 + 必应 + Qwant + Startpage + DuckDuckGo + Hacker News + Reddit + ArXiv，无需 API Key
author: joansongjr
author_url: https://github.com/joansongjr
repository: https://github.com/joansongjr/cn-web-search
license: MIT
tags:
  - search
  - chinese
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
  - no-api-key
  - free
  - 中文搜索
  - 学术搜索
  - 防封
---

# 中文网页搜索 (CN Web Search)

多引擎聚合搜索，零配置，无需 API Key。**8+ 搜索引擎**，中文/英文/科技/学术全覆盖。

## 搜索引擎总览

| 类别 | 引擎 | 状态 | 说明 |
|------|------|------|------|
| **中文主引擎** | 360 搜索 | 主 | 可能被限 |
| **中文备用** | 搜狗网页 | 备用1 | 360 被限时用 |
| **中文备用** | 必应中文 | 备用2 | 最稳定 |
| **英文主引擎** | DuckDuckGo Lite | 主 | 零反爬 |
| **英文备用** | Qwant | 备用1 | 欧洲隐私引擎 |
| **英文备用** | Startpage | 备用2 | 荷兰引擎 |
| **英文备用** | 必应英文 | 备用3 | 最后防线 |
| **科技** | Hacker News | 专用 | API 直接返回 JSON |
| **社区** | Reddit | 专用 | 真实用户讨论 |
| **学术** | ArXiv | 专用 | 免费论文 |

## 防封策略

### 请求间隔
- 每次搜索后 **等待 3-5 秒**
- 连续请求不超过 3 次
- 超过后等待 30 秒

### 备用切换逻辑
```
中文: 360 → 搜狗 → 必应
英文: DDG → Qwant → Startpage → 必应
```

---

## 1. 中文搜索

### 1.1 360 搜索（主）

```
https://m.so.com/s?q=QUERY
```

### 1.2 搜狗网页（备用1）

```
https://www.sogou.com/web?query=QUERY
```

### 1.3 必应中文（备用2）

```
https://cn.bing.com/search?q=QUERY
```

---

## 2. 英文搜索

### 2.1 DuckDuckGo Lite（主）

```
https://lite.duckduckgo.com/lite/?q=QUERY
```

### 2.2 Qwant（备用1）⭐ 新增

欧洲隐私搜索引擎，无需 API，完全免费！

```
https://www.qwant.com/?q=QUERY&t=web
```

### 2.3 Startpage（备用2）⭐ 新增

荷兰搜索引擎，无追踪！

```
https://www.startpage.com/do/search?q=QUERY&cluster=web
```

### 2.4 必应英文（备用3）

```
https://www.bing.com/search?q=QUERY
```

---

## 3. 科技新闻：Hacker News

API 直接返回 JSON，最方便！

```
https://hn.algolia.com/api/v1/search?query=QUERY&tags=story&hitsPerPage=10
```

---

## 4. 社区讨论：Reddit

```
https://www.reddit.com/search.json?q=QUERY&limit=10
```

---

## 5. 学术论文：ArXiv

```
http://export.arxiv.org/api/query?search_query=all:QUERY&max_results=5
```

---

## 使用示例

### 搜"A股产业链梳理"

```
# 中文 - 360
web_fetch(url="https://m.so.com/s?q=A股产业链梳理", extractMode="text", maxChars=12000)

# 被限 → 搜狗
web_fetch(url="https://www.sogou.com/web?query=A股产业链梳理", extractMode="text", maxChars=10000)

# 再被限 → 必应
web_fetch(url="https://cn.bing.com/search?q=A股产业链梳理", extractMode="text", maxChars=10000)
```

### 搜英文科技新闻

```
# DDG
web_fetch(url="https://lite.duckduckgo.com/lite/?q=semiconductor+industry", extractMode="text", maxChars=8000)

# 被限 → Qwant
web_fetch(url="https://www.qwant.com/?q=semiconductor+industry&t=web", extractMode="text", maxChars=10000)
```

---

## 为什么加 Qwant 和 Startpage？

| 引擎 | 优势 |
|------|------|
| **Qwant** | 欧洲最大隐私搜索引擎，无追踪，无需 API |
| **Startpage** | 荷兰引擎，Google 结果但无追踪 |
| **必应** | 微软背书，结果准，反爬最松 |

这三个都是**不需要 API Key** 的免费引擎，适合作为英文搜索的备用！

---

## 搜索技巧

- 精确短语：`q=%22深度学习%22`
- 加年份：`Python 教程 2025`
- HN 加 tags：`tags=story` 或 `tags=ask_hn`
- ArXiv 搜分类：`search_query=cat:cs.AI`

---

## 更新日志

### v0.4.0
- ✅ 增加 Qwant 搜索（欧洲隐私引擎）
- ✅ 增加 Startpage 搜索（荷兰无追踪）
- ✅ 增加必应英文作为备用
- ✅ 优化英文搜索备用链

### v0.3.0
- ✅ 防封策略 + 搜狗 + 必应中文

### v0.2.0
- ✅ HN + Reddit + ArXiv
