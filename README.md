# 🤖 AI Daily Brief

每天早上自动抓取 AI / Robotics / Agent 领域的最新动态，由 Claude Opus 生成深度分析，发送到你的邮箱。

## 效果预览

每封邮件包含五个部分：

| 板块 | 内容 |
|------|------|
| 📌 重点新闻 | 10-15 条精选，每条附意义分析和关联判断 |
| 📈 趋势分析 | 2-3 个跨文章归纳的行业/技术趋势及预判 |
| 🔬 值得深挖 | 精选 arxiv 论文，说明核心贡献和阅读重点 |
| 📖 今日推荐博客 | 1 篇研究员博客深度导读，含核心观点和适读人群 |
| 💡 今日信号 | 一句话最关键判断 |

## 信息来源

**新闻**（24 小时窗口）
- OpenAI Blog、Google DeepMind、Hugging Face
- The Verge AI、MIT Technology Review、VentureBeat、TechCrunch
- arxiv cs.AI、arxiv cs.RO

**研究员博客**（72 小时窗口）
- Interconnects (Nathan Lambert)、Ahead of AI (Sebastian Raschka)
- Import AI (Jack Clark)、The Gradient、One Useful Thing (Ethan Mollick)
- AI Snake Oil、Lilian Weng、Last Week in AI

## 部署

### 1. Fork / Clone 这个仓库

### 2. 获取 Gmail 应用密码

1. Google 账号 → 安全 → 开启两步验证
2. 搜索 "App Passwords" → 生成 → 保存 16 位密码

### 3. 在 GitHub 仓库添加 Secrets

进入仓库 → **Settings → Secrets and variables → Actions**，添加：

| Secret | 说明 |
|--------|------|
| `ANTHROPIC_API_KEY` | Anthropic API Key |
| `GMAIL_USER` | 发件 Gmail 地址 |
| `GMAIL_APP_PASSWORD` | 上一步生成的应用密码 |
| `RECIPIENT_EMAIL` | 收件邮箱（可与发件相同） |

### 4. 手动触发测试

仓库 → **Actions → Daily AI News → Run workflow**

之后每天 **06:00 UTC（英国夏令时 07:00 BST）** 自动运行。

## 个性化配置

编辑 [`config.yml`](./config.yml)，推送到 GitHub 即生效，**无需改代码**。

```yaml
# 关注主题（引导 Claude 的分析方向）
topics:
  - robotics
  - AI agents
  - large language models

# arxiv 过滤关键词
arxiv_keywords:
  - robot
  - agent
  - ...

# 新闻来源（注释掉某行即禁用）
news_feeds:
  OpenAI Blog: https://openai.com/blog/rss.xml
  ...

# 博客来源
blog_feeds:
  Interconnects (Nathan Lambert): https://www.interconnects.ai/feed
  ...

# 运行参数
digest:
  model: claude-opus-4-7      # 或 claude-sonnet-4-6（更便宜）
  news_hours: 24
  blog_hours: 72
  output_language: 中文
```

## 费用估算

| 模型 | 每天 | 每月 |
|------|------|------|
| Claude Opus 4.7 | ~$0.67 | ~$20 |
| Claude Sonnet 4.6 | ~$0.05 | ~$1.5 |

GitHub Actions 完全免费（公共仓库无限制，私有仓库每月 2000 分钟免费额度）。

## 技术栈

- **运行环境**：GitHub Actions（定时触发）
- **抓取**：`feedparser`（RSS）
- **分析**：Claude Opus via Anthropic API
- **推送**：Gmail SMTP
- **配置**：`config.yml`（YAML）
