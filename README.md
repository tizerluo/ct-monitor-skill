# 📡 CT Monitor — 加密市场全栈情报分析师

> 整合 5000+ KOL 推文、实时新闻、RSS、CoinGecko 价格数据，提取 Alpha 信号、识别新兴叙事、生成 AI 简报。

---

## 这是什么？

CT Monitor 是一个专为加密市场设计的 OpenClaw Skill。它连接到一个持续运行的后端服务，该服务：

- **实时监控** 5000+ 加密 KOL 的推文（每 30 分钟 ~ 24 小时同步一次，按影响力分级）
- **聚合多源资讯**：AI 评分新闻 + 精选 RSS 订阅，自动去重
- **追踪价格数据**：CoinGecko 实时价格 + 趋势币分析 + KOL 提及关联
- **提取 Alpha 信号**：基于 KOL 影响力加权，识别高频提及的代币和叙事
- **生成 AI 简报**：由 Grok 4.1 Fast 整合多源数据，生成可操作的市场分析

安装后，你可以直接用自然语言向 OpenClaw 提问，它会自动调用相应的 API 并整合分析结果。

---

## 能做什么？

| 场景 | 示例问题 |
| :--- | :--- |
| 📰 **早间情报** | "给我一份今天的加密市场早报" |
| 🔍 **Alpha 信号** | "最近 1 小时有什么值得关注的信号？" |
| 👤 **KOL 调查** | "Vitalik 最近在关注什么？" |
| 🏗️ **项目尽调** | "帮我快速调查一下 Hyperliquid" |
| 🚨 **安全预警** | "有没有最新的 Hack 或 Rug 消息？" |
| 💰 **价格查询** | "BTC 现在多少钱？过去 24 小时涨了多少？" |
| 📈 **趋势分析** | "现在什么币最热？KOL 们在讨论什么？" |
| 📅 **定投辅助** | "帮我分析一下本周市场，给出定投建议" |

---

## 快速开始

### Step 1：获取 API Key

访问 [ctmon.xyz](https://ctmon.xyz) 注册账号并获取 API Key。

### Step 2：在 OpenClaw 中安装 Skill

```
/skill install ct-monitor
```

或者通过 ClawHub 搜索 "CT Monitor" 安装。

### Step 3：配置 API Key

安装后，OpenClaw 会提示你输入 `CT_MONITOR_API_KEY`，填入你在 Step 1 获取的 API Key 即可。

**验证安装**：
```
检查一下 CT Monitor 的系统状态
```

OpenClaw 应该返回同步状态和最后更新时间。

---

## 使用场景与组合拳

CT Monitor 的真正价值在于**多源数据组合**。以下是 6 个最常用的场景，每个场景都展示了如何将多个 API 组合使用，产出远超单一查询的洞察。

### 🌅 场景一：早间情报简报（每日必做）

**你说**：
> 给我一份今天的加密市场早报，包括市场情绪、热门叙事和值得关注的代币

**OpenClaw 会做**：
1. 调用 `/brief/generate?hours=24` 获取 AI 综合简报
2. 调用 `/price/trending?hours=24` 获取趋势币 + KOL 提及分析
3. 调用 `/signals/recent?hours=6` 获取最近 6 小时高频信号
4. 整合三份数据，生成结构化早报

**你会得到**：市场整体情绪 + 今日最热叙事 Top 3 + 值得关注的代币（附理由）+ 今日风险提示

💡 **设置定时推送**：让 OpenClaw 每天早上 8 点自动发送到 Telegram

---

### 🎯 场景二：Alpha 信号深挖（发现机会时）

**你说**：
> 最近 1 小时有什么 Alpha 信号？帮我深挖一下最强的那个

**OpenClaw 会做**：
1. 调用 `/signals/recent?hours=1` 发现高频提及代币（如 $PENGU）
2. 调用 `/price/token?symbol=PENGU` 查当前价格和涨跌幅
3. 调用 `/tweets/feed` 过滤出所有提及 $PENGU 的 KOL 推文
4. 调用 `/info/feed?coin=PENGU` 查相关新闻和 RSS
5. 调用 `/users/top` 评估提及 KOL 的影响力权重
6. 综合分析，给出信号强度评级和操作建议

**你会得到**：信号强度评级（强/中/弱）+ KOL 质量评估 + 价格背景 + 新闻佐证 + 操作建议（附风险提示）

---

### 👤 场景三：KOL 深度画像（研究某个 KOL）

**你说**：
> 帮我深度分析一下 @cobie，他最近在关注什么，投资逻辑是什么？

**OpenClaw 会做**：
1. 调用 `/twitter/realtime?username=cobie` 获取最新实时推文
2. 调用 `/tweets/recent?username=cobie` 获取历史推文（更长时间跨度）
3. 调用 `/tweets/search?keyword=cobie` 搜索其他 KOL 对他的引用和评论
4. 综合三个维度，生成 KOL 画像

**你会得到**：近期关注赛道/项目 + 核心观点提炼（Bullish/Bearish 立场）+ 投资逻辑分析 + 影响力评估 + 值得关注的观点

---

### 🏗️ 场景四：项目尽调（快速全面调查）

**你说**：
> 帮我快速调查一下 Hyperliquid，我想了解社区热度、KOL 态度和价格表现

**OpenClaw 会做**：
1. 调用 `/tweets/feed` 过滤出所有提及 Hyperliquid/HYPE 的 KOL 推文
2. 调用 `/info/feed?coin=HYPE` 查相关新闻和 RSS
3. 调用 `/price/token?symbol=HYPE` 查价格数据
4. 调用 `/signals/recent?hours=24` 查过去 24H 信号
5. 综合生成尽调报告

**你会得到**：社区热度评估 + KOL 情绪分布（Bullish/Bearish 比例）+ 价格表现分析 + 近期催化剂 + 主要风险点

---

### 🚨 场景五：安全预警响应（发现风险时）

**你说**：
> 我看到有人说某个协议被黑了，帮我快速确认一下，评估影响

**OpenClaw 会做**：
1. 调用 `/tweets/feed` 过滤 hack/exploit/rug 相关推文，确认事件
2. 调用 `/info/feed` 查看新闻报道
3. 调用 `/price/token` 查看受影响代币价格
4. 调用 `/signals/recent?hours=0.25` 查看最近 15 分钟恐慌信号
5. 综合评估，给出紧急程度评级

**你会得到**：事件确认（是否属实）+ 影响范围评估 + 受影响资产分析 + 紧急程度评级（高/中/低）+ 建议操作

💡 **设置实时监控**：让 OpenClaw 每 15 分钟检查一次，发现安全事件立即推送

---

### 📅 场景六：定投决策辅助（每周复盘）

**你说**：
> 帮我做一个本周的市场复盘，给出下周的定投建议

**OpenClaw 会做**：
1. 调用 `/brief/generate?hours=24` 获取最新市场简报
2. 调用 `/price/trending?hours=24` 查过去 24H 趋势币
3. 调用 `/price/summary` 查主流币价格总览
4. 调用 `/signals/recent?hours=6` 查近期信号汇总
5. 综合分析，生成投资决策报告

**你会得到**：市场趋势判断（牛/熊/震荡）+ 值得关注的赛道 + 主流币配置建议 + 风险提示 + 定投策略建议

---

## 定时推送示例

在 OpenClaw 中设置 Cron 任务，让 CT Monitor 自动工作：

**每日早报（每天 8:00）**：
```
每天早上 8 点，调用 CT Monitor 生成过去 24 小时的市场简报（包含 AI 简报 + 趋势币 + 信号），
整理成中文要点，通过 Telegram 发送给我。
```

**实时信号预警（每 15 分钟）**：
```
每 15 分钟检查一次 CT Monitor 的最新信号，
若有 kol_count >= 3 的信号，立即发送 Telegram 预警，包含代币名称、信号强度和相关 KOL。
```

**每周复盘（每周日 20:00）**：
```
每周日晚上 8 点，调用 CT Monitor 生成本周市场复盘报告，
包含市场趋势、热门赛道、值得关注的代币，通过 Telegram 发送给我。
```

---

## 定价说明

CT Monitor 按调用次数计费，费用从你的账户余额中扣除：

| 端点 | 费用 | 说明 |
| :--- | :--- | :--- |
| `/brief/generate` hours=1 | 6¢ | 1H 快讯（Grok 4.1 Fast） |
| `/brief/generate` hours=8 | 4¢ | 8H 简报 |
| `/brief/generate` hours=12/24 | 2¢ | 12/24H 简报 |
| `/signals/recent` hours<2 | 3¢ | 实时数据（6551 源） |
| `/signals/recent` hours≥2 | 1¢ | 历史数据库 |
| `/twitter/realtime` | 2¢ | 实时推文（6551 源） |
| `/price/token` | 1¢ | 代币价格查询 |
| `/price/trending` | 1¢ | 趋势币分析 |
| `/price/summary` | 1¢ | 市场总览 |
| `/info/feed` | 1¢ | 统一资讯流 |
| `/tweets/feed` `/tweets/recent` `/tweets/search` | 免费 | 历史数据库查询 |

**典型场景费用**：
- 早间情报简报：约 4¢/次
- Alpha 信号深挖：约 6¢/次
- 每日定时推送：约 $1.2/月

---

## 常见问题

**Q：数据有多新鲜？**
A：KOL 推文按影响力分级同步：Ultra High（53人）每 30 分钟，High（196人）每 1 小时，Normal（1100人）每 4 小时，Low（500人）每 24 小时。实时推文通过 `/twitter/realtime` 端点获取，延迟约 1-2 分钟。

**Q：监控了哪些 KOL？**
A：目前监控 5000+ 加密 KOL，涵盖 Layer1/Layer2/DeFi/AI/Meme 等 27 个赛道。你也可以通过 `POST /subscriptions/?username=XXX` 添加自定义监控。

**Q：API 返回空数据怎么办？**
A：若返回 `[]`，通常是该时间窗口内暂无相关数据，可以扩大时间范围（增大 hours 参数）或稍后重试。

**Q：如何充值？**
A：访问 [ctmon.xyz](https://ctmon.xyz) 的账户页面进行充值。

**Q：支持哪些语言的分析？**
A：API 返回原始数据（主要是英文推文），AI 分析和整合输出支持中文。

---

## 相关链接

- 官网：[ctmon.xyz](https://ctmon.xyz)
- API 文档：[api.ctmon.xyz/docs](https://api.ctmon.xyz/docs)
- Dashboard：[dashboard.ctmon.xyz](https://dashboard.ctmon.xyz)
