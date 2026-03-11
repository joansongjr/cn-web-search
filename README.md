# CN Web Search - 中文网页搜索

给 AI agent 的多引擎搜索能力。聚合 360 搜索 + DuckDuckGo + Hacker News + Reddit + ArXiv，中英文自动切换，**零配置、无需 API Key**。

## 为什么需要这个？

ClawHub 上现有的搜索 skill 都是英文引擎，搜中文内容效果很差。

CN Web Search 覆盖 5 大搜索引擎：
- 🇨🇳 **360 搜索** — 中文内容首选
- 🌍 **DuckDuckGo** — 英文通用搜索
- 📰 **Hacker News** — 科技/编程趋势
- 💬 **Reddit** — 社区真实讨论
- 📚 **ArXiv** — 学术论文

## 安装

```bash
clawhub install cn-web-search
```

## 特点

- 🆓 **完全免费** — 不需要任何 API Key
- 🇨🇳 **中文优化** — 360 搜索返回高质量中文结果
- 🌍 **英文支持** — DDG + HN + Reddit + ArXiv
- 📦 **零依赖** — 纯 SKILL.md，利用 OpenClaw 内置工具
- 🔒 **安全** — 无可执行代码，不会被 VirusTotal 标记

## 搜索引擎对比

| 引擎 | 适用场景 | 示例 |
|------|---------|------|
| 360 搜索 | 中文资讯、新闻、产品 | "英伟达财报"、"手机推荐" |
| DDG Lite | 英文通用搜索 | "how to use API" |
| Hacker News | 科技趋势、编程讨论 | "LLM 推理优化" |
| Reddit | 产品评价、经验分享 | "iPhone 16 好不好" |
| ArXiv | 学术论文 | "transformer 架构" |

## 使用示例

安装后直接提问：

```
"搜一下光模块最新消息"
"Search Hacker News for LLM discussions"
"找一下 ArXiv 上关于扩散模型的论文"
"Reddit 上 Python 异步编程的讨论"
```

## 进阶使用

### 1. 搜索 + 抓取完整内容

```bash
# 第一步：搜结果
web_fetch(url="https://m.so.com/s?q=英伟达财报", extractMode="text", maxChars=12000)

# 第二步：抓全文
web_fetch(url="https://finance.sina.com.cn/...", extractMode="markdown", maxChars=20000)
```

### 2. 组合多引擎调研

```bash
# 中文调研
web_fetch(url="https://m.so.com/s?q=AI+手机", extractMode="text", maxChars=12000)

# 英文科技趋势
web_fetch(url="https://hn.algolia.com/api/v1/search?query=AI+phones&tags=story&hitsPerPage=5", extractMode="text", maxChars=5000)

# 真实用户评价
web_fetch(url="https://www.reddit.com/search.json?q=AI+phones+review&limit=5", extractMode="text", maxChars=5000)
```

### 3. 学术研究

```bash
# 搜论文
web_fetch(url="http://export.arxiv.org/api/query?search_query=all:diffusion+model&max_results=5", extractMode="text", maxChars=5000)

# 下载 PDF（论文 ID: 2310.12345）
# URL 格式: https://arxiv.org/pdf/2310.12345.pdf
```

## 常见问题

### Q: 为什么会自动选择不同引擎？
A: SKILL.md 中的 AI 指令会根据查询内容类型自动选择最适合的引擎。你也可以指定引擎。

### Q: 结果数量不够怎么办？
A: 调整参数：
- 360：`maxChars=15000`
- HN：`hitsPerPage=20`
- Reddit：`limit=20`

### Q: 遇到限速怎么办？
A: 等待 3-5 秒后重试，通常会自动恢复。

### Q: 如何获取完整文章内容？
A: 使用"搜索-抓取"模式：先搜到 URL，再用 `extractMode="markdown"` 抓取全文。

## 更新日志

### v0.2.0
- ✅ 增加 Hacker News 搜索
- ✅ 增加 Reddit 搜索
- ✅ 增加 ArXiv 学术搜索
- ✅ 增加组合搜索策略说明
- ✅ 优化搜索技巧

### v0.1.0
- 🎉 初始版本
- ✅ 360 搜索 + DuckDuckGo 双引擎

## License

MIT

## 作者

joansongjr — https://github.com/joansongjr/cn-web-search
