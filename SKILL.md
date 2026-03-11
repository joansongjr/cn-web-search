---
name: cn-web-search
version: 0.1.0
description: 中文网页搜索 - 聚合 360 搜索 + DuckDuckGo，无需 API Key，中英文双引擎自动切换
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
  - no-api-key
  - free
  - 中文搜索
---

# 中文网页搜索 (CN Web Search)

中英文双引擎搜索，零配置，无需 API Key。中文用 360 搜索，英文用 DuckDuckGo Lite。

## 搜索引擎选择

| 查询语言 | 搜索引擎 | 原因 |
|---------|---------|------|
| **中文** | 360 搜索移动版 | 中文内容质量最好，不需要 JS 渲染，无反爬验证 |
| **英文** | DuckDuckGo Lite | 纯 HTML，零反爬，结果来自 Bing 索引 |

**判断规则：** 查询中包含中文字符 → 用 360 搜索；否则 → 用 DuckDuckGo。

---

## 中文搜索：360 搜索

### 请求方式

```
web_fetch(url="https://m.so.com/s?q=QUERY", extractMode="text", maxChars=12000)
```

- `QUERY` 需要 URL 编码（中文直接编码即可）
- 使用 `extractMode="text"` 获取纯文本，方便解析

### 示例

```
web_fetch(url="https://m.so.com/s?q=英伟达最新财报", extractMode="text", maxChars=12000)
```

### 解析结果

返回的文本中，搜索结果通常包含以下结构：
- **标题** — 出现在独立行，通常带有查询关键词的高亮（`<em>` 标签在 text 模式下已去除）
- **摘要** — 紧跟标题下方，1-3 行描述
- **来源和日期** — 在摘要下方，格式如 "新浪财经 2025年11月20日"

提取前 5-10 条有效结果返回给用户。跳过广告和推荐卡片（如"相关人物""相关机构"等）。

### 中文搜索特点

- ✅ 结果来源丰富：东方财富、新浪财经、凤凰网、知乎、百度百科等
- ✅ 有日期信息，可判断时效性
- ✅ 摘要质量高，通常足够回答问题
- ❌ 不支持时间范围筛选

---

## 英文搜索：DuckDuckGo Lite

### 请求方式

```
web_fetch(url="https://lite.duckduckgo.com/lite/?q=QUERY", extractMode="text", maxChars=8000)
```

- 用 `+` 代替空格，或使用 URL 编码
- 使用 `extractMode="text"` 获取干净的纯文本结果

### 示例

```
web_fetch(url="https://lite.duckduckgo.com/lite/?q=NVIDIA+latest+earnings", extractMode="text", maxChars=8000)
```

### 区域过滤

添加 `&kl=REGION` 参数：
- `us-en` — 美国
- `uk-en` — 英国
- `au-en` — 澳大利亚
- `de-de` — 德国
- `fr-fr` — 法国
- `hk-tzh` — 香港（中文）

### 解析结果

返回文本中，结果以编号列表出现：
- 每条结果包含标题、URL 和摘要
- 前 1-2 条可能是广告（标记为 "Sponsored link"），跳过
- 有效结果从第一条非广告结果开始

---

## 双引擎搜索（可选）

当需要最全面的结果时，可以同时搜两个引擎然后合并：

1. 用 360 搜索搜中文版本的关键词
2. 用 DDG 搜英文版本的关键词
3. 合并去重，按相关性排序返回

适用于：国际性话题（如"英伟达财报"同时需要中英文信息源）。

---

## 搜索-抓取模式 (Search → Fetch)

搜索只返回摘要。如果需要完整内容：

1. **搜索** — 用上面的方式获取搜索结果列表
2. **筛选** — 挑出最相关的 URL（通常 2-3 个）
3. **抓取** — 用 `web_fetch(url="目标URL", extractMode="markdown")` 获取完整页面内容

### 示例流程

```
# 第一步：搜索
web_fetch(url="https://m.so.com/s?q=英伟达2025财报分析", extractMode="text", maxChars=12000)

# 第二步：抓取最相关的结果页面
web_fetch(url="https://finance.sina.com.cn/...", extractMode="markdown", maxChars=20000)
```

---

## 不可用的搜索引擎（已测试）

| 引擎 | 原因 |
|------|------|
| **百度** | 有安全验证/验证码，会被拦截 |
| **Google** | 有 captcha 人机验证 |
| **搜狗** | 中文编码问题，返回乱码 |
| **头条搜索** | 需要 JS 渲染，纯 HTML 没有内容 |

---

## Tips

- 360 搜索用 `maxChars=12000` 可以拿到约 8-10 条结果
- DDG 用 `maxChars=8000` 可以拿到约 10 条结果
- 搜索精确短语时用引号：`q=%22精确短语%22`
- 加限定词可提高精度：加入年份、网站名、具体术语
- 如果 360 搜索偶尔被限速，等几秒重试即可

## 局限性

- 无法按时间范围过滤结果
- 纯文本结果，无图片/视频
- 360 搜索偶尔返回不相关的推荐内容（需过滤）
- 搜索频率过高可能被临时限速
