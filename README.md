# CN Web Search - 中文网页搜索

**8+ 搜索引擎聚合**，中文/英文/科技/学术全覆盖。零配置、无需 API Key。

## 核心优势

- 🛡️ **防封策略** — 请求间隔 + 多备用源
- 🔄 **8+ 引擎** — 360/搜狗/必应/Qwant/Startpage/DDG/HN/Reddit/ArXiv
- 🇨🇳 **中文优化** — 三重备用源（搜狗→必应）
- 🌍 **英文支持** — Qwant + Startpage + 必应
- 📦 **零依赖** — 纯 SKILL.md
- 🔒 **安全** — 无可执行代码

## 搜索引擎

| 类别 | 引擎 | 说明 |
|------|------|------|
| 中文 | 360 搜索 | 主引擎，可能被限 |
| 中文 | 搜狗网页 | 备用1 |
| 中文 | 必应中文 | 备用2 |
| 英文 | DuckDuckGo | 主引擎 |
| 英文 | Qwant | 欧洲隐私引擎 ⭐ |
| 英文 | Startpage | 荷兰无追踪 ⭐ |
| 英文 | 必应 | 备用 |
| 科技 | Hacker News | API 直接返回 JSON |
| 社区 | Reddit | 真实讨论 |
| 学术 | ArXiv | 免费论文 |

## 安装

```bash
clawhub install cn-web-search
```

## 使用示例

```
"搜一下半导体产业链"
"Search Qwant for AI news"
"Hacker News 上 LLM 的讨论"
"找 ArXiv 上扩散模型论文"
```

## 更新日志

### v0.4.0
- ✅ 增加 Qwant（欧洲隐私引擎）
- ✅ 增加 Startpage（荷兰无追踪）
- ✅ 优化英文备用链

### v0.3.0
- ✅ 防封策略 + 搜狗 + 必应中文

### v0.2.0
- ✅ HN + Reddit + ArXiv

## License

MIT
