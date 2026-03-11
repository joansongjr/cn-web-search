# CN Web Search - 中文网页搜索

**14+ 搜索引擎聚合**，免费+付费混合。包含公众号文章搜索！

## 引擎分类

### 免费引擎（无需配置）
- 公众号：搜狗微信、必应索引 ⭐
- 中文：360、搜狗、必应
- 英文：DDG、Qwant、Startpage、必应
- 技术：Stack Overflow、GitHub Trending
- 专用：Hacker News、Reddit、ArXiv
- 投资：东方财富
- 深度：财新
- 知识：Wolfram Alpha

### 付费引擎（需要 API Key）
| 引擎 | 要求 | 免费额度 |
|------|------|---------|
| **Tavily** | TAVILY_API_KEY | 1000次/月 ⭐ |

## 安装

```bash
clawhub install cn-web-search
```

## 使用示例

```
# 免费搜索
"搜公众号 英伟达 文章"

# Tavily（需要 Key）
export TAVILY_API_KEY=你的Key
web_fetch(url="https://api.tavily.com/search?api_key=$TAVILY_API_KEY&q=AI&max_results=10", ...)
```

## 更新日志

### v0.8.0
- ✅ Tavily（付费，需要 API Key）

### v0.7.0
- ✅ 公众号搜索

### v0.6.0
- ✅ 财新 + Wolfram Alpha

## License

MIT
