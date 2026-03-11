# CN Web Search - 中文网页搜索

给 AI agent 的中文搜索能力。聚合 360 搜索 + DuckDuckGo，中英文自动切换，**零配置、无需 API Key**。

## 为什么需要这个？

ClawHub 上现有的搜索 skill（Brave Search、Tavily、DDG）都是英文搜索引擎，搜中文内容效果很差。

CN Web Search 用 360 搜索作为中文引擎，能直接返回新浪财经、东方财富、知乎、凤凰网等高质量中文内容。

## 安装

```bash
clawhub install cn-web-search
```

## 特点

- 🆓 **完全免费** — 不需要任何 API Key
- 🇨🇳 **中文优化** — 360 搜索返回高质量中文结果
- 🌍 **中英双语** — 自动判断语言，切换搜索引擎
- 📦 **零依赖** — 纯 SKILL.md，利用 OpenClaw 内置的 web_fetch 工具
- 🔒 **安全** — 无可执行代码，不会被 VirusTotal 标记

## 搜索引擎

| 语言 | 引擎 | 来源 |
|------|------|------|
| 中文 | 360 搜索移动版 | 新浪、东方财富、知乎、凤凰网等 |
| 英文 | DuckDuckGo Lite | Bing 索引 |

## 使用示例

安装后 AI agent 会自动使用。你只需要正常提问：

- "搜一下英伟达最新财报"
- "Search for latest AI research papers"
- "帮我查一下上海今天天气"

## License

MIT
