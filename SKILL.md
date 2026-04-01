---
name: cn-web-search
version: 2.3.0
description: 中文网页搜索 - 聚合 17 个免费搜索引擎 + 债券/利率市场免费数据接口，无需 API Key，纯网页抓取，支持公众号/财经/技术/学术/知识/债券搜索。
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
  - stackoverflow
  - github
  - caixin
  - baidu
  - brave-search
  - yahoo
  - mojeek
  - toutiao
  - jisilu
  - wikipedia
  - no-api-key
  - free
  - 中文搜索
  - 百度
  - 头条搜索
  - 东方财富
  - A股
  - 财经
  - 技术搜索
  - 多引擎
  - 聚合搜索
  - 免费无需API
  - 投资
  - 知识百科
  - 债券
  - 信用债
  - 中债估值
  - 国开债
  - 收益率曲线
  - bond
---

# 中文网页搜索 (CN Web Search)

> **⚡ 安装:**
> ```bash
> clawhub install cn-web-search
> ```

多引擎聚合搜索，**全部免费，无需 API Key，纯网页抓取**。17 个引擎覆盖中英文、公众号、技术、财经、知识百科；另含经过实测可用的**债券/利率市场免费数据接口**。

## 引擎总览（17 个）

| 类别 | 引擎 | 数量 |
|------|------|------|
| 公众号 | 搜狗微信、必应索引 | 2 |
| 中文综合 | 360、搜狗、必应中文、百度、头条搜索 | 5 |
| 英文综合 | DDG Lite、Qwant、Startpage、必应英文、Yahoo、Brave Search、Mojeek | 7 |
| 技术社区 | Stack Overflow、GitHub Trending | 2 |
| 财经/投资 | 东方财富、集思录、财新 | 3 |
| 知识百科 | Wikipedia 中文、Wikipedia 英文 | 2 |

> 全部通过 `web_fetch` 抓取网页，零 API 依赖。

---

## 1. 公众号搜索

### 1.1 搜狗微信

```
https://weixin.sogou.com/weixin?type=2&query=QUERY&page=1
```

### 1.2 必应公众号索引

```
https://cn.bing.com/search?q=site:mp.weixin.qq.com+QUERY
```

---

## 2. 中文综合搜索

### 2.1 360 搜索

```
https://m.so.com/s?q=QUERY
```

### 2.2 搜狗网页

```
https://www.sogou.com/web?query=QUERY
```

### 2.3 必应中文

```
https://cn.bing.com/search?q=QUERY
```

### 2.4 百度

```
https://www.baidu.com/s?wd=QUERY
```

中文搜索覆盖最全，结果丰富。

### 2.5 头条搜索

```
https://so.toutiao.com/search?keyword=QUERY
```

字节跳动旗下，中文资讯和短视频内容强。

---

## 3. 英文综合搜索

### 3.1 DuckDuckGo Lite

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

### 3.5 Yahoo

```
https://search.yahoo.com/search?p=QUERY
```

老牌英文搜索引擎，结果稳定。

### 3.6 Brave Search

```
https://search.brave.com/search?q=QUERY
```

独立索引（非 Bing/Google 代理），隐私友好，结果质量高。

### 3.7 Mojeek

```
https://www.mojeek.com/search?q=QUERY
```

独立爬虫索引，不依赖任何大厂，适合多样化结果。

---

## 4. 技术社区

### 4.1 Stack Overflow

```
https://stackoverflow.com/search?q=QUERY
```

### 4.2 GitHub Trending

```
https://github.com/trending?since=weekly
```

---

## 5. 财经/投资

### 5.1 东方财富

```
https://search.eastmoney.com/search?keyword=QUERY
```

### 5.2 集思录

```
https://www.jisilu.cn/explore/?keyword=QUERY
```

投资社区，可转债、基金、LOF 等投资品种讨论。

### 5.3 财新

```
https://search.caixin.com/search/?keyword=QUERY
```

---

## 6. 债券市场免费数据接口（实测可用）

> 以下接口经过实测验证，无需登录、无需 API Key，直接 `web_fetch` 即可获取结构化数据。

### 6.1 中债网收益率曲线（✅ 实测可用）

**数据源**：中国债券信息网 `cbrc` 接口
**可获取数据**：国债、商业银行普通债(AAA)、中短期票据(AAA) 各期限收益率

```
https://yield.chinabond.com.cn/cbweb-cbrc-web/cbrc/queryGjqxInfo?workTime=DATE&locale=zh_CN
```

- `DATE` 替换为目标日期，格式 `yyyy-MM-dd`，如 `2026-03-13`
- 返回曲线覆盖：3M / 6M / 1Y / 3Y / 5Y / 7Y / 10Y / 30Y
- **用途**：计算国开债基准收益率、信用债利差基准

```python
# 示例：获取2026-03-13的收益率曲线
web_fetch(
    url="https://yield.chinabond.com.cn/cbweb-cbrc-web/cbrc/queryGjqxInfo?workTime=2026-03-13&locale=zh_CN",
    extractMode="text",
    maxChars=5000
)
# 返回示例（国债）：3M:1.2309% / 6M:1.2400% / 1Y:1.2768% / 3Y:1.3704% / 5Y:1.5619% / 10Y:1.8143%
# 返回示例（商业银行AAA）：1Y:1.5460% / 3Y:1.7036% / 5Y:1.7968% / 10Y:2.1933%
# 返回示例（中短期票据AAA）：1Y:1.6248% / 3Y:1.8002% / 5Y:1.9308% / 10Y:2.2994%
```

> ⚠️ 注意：该接口返回的是 HTML 页面，数据已内嵌在 JS 变量中，`web_fetch` 可直接解析文本获取数值。国开债曲线需通过 `zjlx=g` 参数或访问其他子接口获取，当前接口不含国开债。

---

### 6.2 东方财富债券基本信息（✅ 实测可用）

**数据源**：东方财富行情 API
**可获取数据**：债券代码、简称、面值、期限、利率类型、上市状态

```
https://push2.eastmoney.com/api/qt/stock/get?secid=MARKET.CODE&fields=f43,f57,f58,f59,f60,f107,f111,f112,f118,f152,f177,f179,f180
```

- `MARKET`：`1` = 上交所，`0` = 深交所，`2` = 银行间
- `CODE`：债券代码，如 `243262`（25保利03）

```python
# 示例：查询上交所债券 25保利03(243262) 基本信息
web_fetch(
    url="https://push2.eastmoney.com/api/qt/stock/get?secid=1.243262&fields=f43,f57,f58,f59,f60,f107,f111,f112,f118,f152,f177,f179,f180",
    extractMode="text",
    maxChars=2000
)
# 返回字段：f57=债券代码, f58=债券简称, f60=发行规模, f111=期限类别, f112=期限年数, f118=利率类型, f152=风险等级
```

> ⚠️ 该接口**不含**中债估值、利差、隐含评级、成交量等深度数据，仅返回静态基本属性。

---

### 6.3 东方财富可转债全量数据（✅ 实测可用）

**数据源**：东方财富数据中心
**可获取数据**：代码、名称、评级、发行规模、到期日、票面利率、转股价、转债条款等

```
https://datacenter-web.eastmoney.com/api/data/v1/get?reportName=RPT_BOND_CB_LIST&columns=ALL&pageNumber=PAGE&pageSize=50
```

> ⚠️ 仅覆盖**可转债**，不含信用债（中票/企业债/公司债）。

```python
# 示例：获取可转债列表第1页
web_fetch(
    url="https://datacenter-web.eastmoney.com/api/data/v1/get?reportName=RPT_BOND_CB_LIST&columns=ALL&pageNumber=1&pageSize=20",
    extractMode="text",
    maxChars=8000
)
```

---

### 6.4 实测不可用的债券数据源（供参考）

| 数据 | 尝试的来源 | 状态 | 原因 |
|------|-----------|------|------|
| 中债估值（单券）| 中债网 | ❌ | 付费授权，无公开接口 |
| 隐含评级（中证/中债）| 中证/中债 | ❌ | 付费授权数据 |
| 银行间成交量/换手率 | 中国货币网 | ❌ 403 | 需浏览器 Cookie |
| 信用债利差 | 各平台 | ❌ | 依赖中债估值，无法派生 |
| 中债流动性指标 | 中债网 | ❌ | 中债专有付费产品 |
| 集思录信用债 | 集思录 | ❌ | 集思录仅有可转债，无信用债 |
| 深交所债券成交 | 深交所 API | ❌ | 接口参数变更，返回空数据 |

---

## 7. 知识百科

### 6.1 Wikipedia 中文

```
https://zh.wikipedia.org/w/index.php?search=QUERY&title=Special:Search
```

中文维基百科，知识查询首选。

### 6.2 Wikipedia 英文

```
https://en.wikipedia.org/w/index.php?search=QUERY&title=Special:Search
```

英文维基百科，信息量最大的免费百科全书。

---

## 使用示例

```
# 中文搜索
web_fetch(url="https://www.baidu.com/s?wd=英伟达财报", extractMode="text", maxChars=12000)
web_fetch(url="https://m.so.com/s?q=英伟达财报", extractMode="text", maxChars=12000)

# 英文搜索
web_fetch(url="https://search.brave.com/search?q=AI+news", extractMode="text", maxChars=8000)
web_fetch(url="https://lite.duckduckgo.com/lite/?q=AI+news", extractMode="text", maxChars=8000)

# 公众号
web_fetch(url="https://weixin.sogou.com/weixin?type=2&query=英伟达&page=1", extractMode="text", maxChars=10000)

# 知识查询
web_fetch(url="https://zh.wikipedia.org/w/index.php?search=量子计算&title=Special:Search", extractMode="text", maxChars=8000)

# 投资
web_fetch(url="https://www.jisilu.cn/explore/?keyword=可转债", extractMode="text", maxChars=8000)
```

---

## 引擎选择建议

| 场景 | 推荐引擎 |
|------|---------|
| 中文通用搜索 | 百度 → 360 → 搜狗 |
| 英文通用搜索 | Brave → DDG → Bing |
| 公众号文章 | 搜狗微信 → 必应索引 |
| 技术问题 | Stack Overflow → GitHub |
| 最新资讯 | 头条搜索 → 百度 |
| A股/投资 | 东方财富 → 集思录 |
| 财经深度 | 财新 |
| 知识/定义 | Wikipedia 中文 → Wikipedia 英文 |
| 隐私优先 | Brave → Mojeek → DDG |
| **利率/收益率曲线** | **中债网 cbrc 接口（6.1节）** |
| **债券基本信息** | **东方财富行情 API（6.2节）** |
| **可转债数据** | **东方财富数据中心（6.3节）** |

---

## 实战对比：有 cn-web-search vs 没有

> 以投研场景为例，问同一个问题：**"英伟达2026年Q1财报业绩如何？"**

### ❌ 没有 cn-web-search（纯模型）

```
回答："我的训练数据有截止日期，无法提供最新财报数据。
      建议您查看英伟达官网 investor.nvidia.com。"
```

**结果：什么有用信息都拿不到。**

### ✅ 装了 cn-web-search（百度 + 360 + 搜狗，3 个免费引擎）

```python
web_fetch(url="https://www.baidu.com/s?wd=英伟达2027财年Q1业绩指引", extractMode="text", maxChars=3000)
web_fetch(url="https://m.so.com/s?q=英伟达2026财报Q1业绩", extractMode="text", maxChars=3000)
web_fetch(url="https://www.sogou.com/web?query=英伟达财报2026Q1业绩预测", extractMode="text", maxChars=3000)
```

**拿到的实时数据（多源交叉验证）：**

| 数据点 | 百度 | 360 | 搜狗 |
|--------|:----:|:---:|:----:|
| FY2026 Q1 营收 441 亿美元 (+69%) | ✅ | ✅ | ✅ |
| FY2026 Q4 营收 681 亿美元 (+73%) | ✅ | ✅ | ✅ |
| FY2026 全年营收 2159 亿美元 (+65%) | ✅ | ✅ | ✅ |
| FY2027 Q1 指引 780 亿（超预期 7%） | ✅ | ✅ | ✅ |
| H20 禁令影响 80 亿美元 | ✅ | ✅ | ✅ |
| 毛利率 75% | ✅ | ✅ | — |
| 黄仁勋："代理式 AI 拐点已到来" | ✅ | — | ✅ |

### 对比总结

| 维度 | 无 Skill | cn-web-search |
|------|:--------:|:-------------:|
| 实时数据 | ❌ | ✅ |
| 数据准确性 | N/A | ✅ 多源交叉验证 |
| 成本 | — | 免费 |
| 投研可用性 | 零 | 营收/利润/指引/管理层表态 |
| 信息来源 | 无 | 百度+360+搜狗+雪球+东方财富 |

> **结论：没有 cn-web-search 的 agent 在投研场景下基本是废的。装上后等于给 agent 开了一扇窗，能看到实时世界——而且完全免费。**

---

## 更新日志

### v2.3.0
- 🏦 新增「债券市场免费数据接口」章节（第6节），收录3个经实测可用的接口
- ✅ 中债网收益率曲线接口：国债/商业银行AAA/中短期票据AAA，各期限实测有效
- ✅ 东方财富债券基本信息 API：静态属性（代码/简称/期限/利率类型）
- ✅ 东方财富可转债全量数据接口
- 📋 补充「实测不可用」对照表：中债估值/隐含评级/成交量/流动性指标均为付费数据
- 🔍 更新引擎选择建议，新增债券场景推荐

### v2.2.0
- 📊 新增「实战对比」章节：有 cn-web-search vs 没有（以英伟达财报投研为例）
- 📈 展示多源交叉验证效果

### v2.1.0
- 🗑️ 移除所有 API 端点引擎（Hacker News、Reddit、ArXiv、DDG API、Wolfram Alpha）
- ✅ 全部 17 个引擎均为纯网页抓取，零 API 依赖
- 📋 更新引擎总览表和选择建议

### v2.0.0
- 🆕 新增 9 个引擎：百度、Yahoo、Brave Search、Mojeek、头条搜索、集思录、Wikipedia 中英文、DDG Instant Answer API
- 📊 引擎总数：13 → 22

### v1.0.0
- ✅ 全新发布！聚合 13+ 免费中文搜索引擎
- ✅ 无需 API Key，真正免费
- ✅ 支持公众号、知乎、财经(A股)、技术搜索
