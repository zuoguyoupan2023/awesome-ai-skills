# Awesome AI Skills

> 精选的 AI Agent Skills 资源索引。涵盖 Claude Code、Codex CLI、Cursor、Gemini CLI 等主流 AI 编码 Agent 的 Skill 生态。
>
> ⚠️ **安全提醒**：安装第三方 skill 前请务必检查其代码。详见 [安全审核指南](SECURITY.md)。
>
> 本仓库是 [CrazyCodeCat](https://github.com/crazycodecat) 生态的一部分，与 [marketplace-skills](https://github.com/crazycodecat/marketplace-skills) 技能仓库和 CCC 浏览器插件联动。

## 什么是 Agent Skill？

Agent Skill 是一个标准化的 AI 指令包（SKILL.md 格式），告诉 AI 如何完成特定领域的任务。详见 [Agent Skills 规范](https://agentskills.so)。

```
my-skill/
├── SKILL.md          # 必需：YAML frontmatter + 指令正文
├── scripts/          # 可选：可执行脚本
├── references/       # 可选：参考文档
└── assets/           # 可选：模板资源
```

---

## 目录

- [官方 Skill 集](#官方-skill-集)
- [精选 Awesome 列表](#精选-awesome-列表)
- [技能市场 / 发现平台](#技能市场--发现平台)
- [按领域分类](#按领域分类)
  - [安全](#安全)
  - [前端开发](#前端开发)
  - [后端开发](#后端开发)
  - [DevOps](#devops)
  - [数据科学 / AI/ML](#数据科学--aiml)
  - [生物信息 / 学术](#生物信息--学术)
  - [法律](#法律)
  - [营销 / 内容创作](#营销--内容创作)
  - [游戏开发](#游戏开发)
- [工具与框架](#工具与框架)
- [安全提醒](#安全提醒)
- [贡献](#贡献)

---

## 官方 Skill 集

| 来源 | 链接 | 说明 |
|------|------|------|
| Anthropic 官方 | [anthropics/skills](https://github.com/anthropics/skills) | Claude Code 官方参考 skill，16 个核心 |
| OpenAI Codex | [Codex CLI 内置](https://github.com/openai/codex) | Codex CLI 默认 skill 集 |
| GitHub Copilot | [github/awesome-copilot](https://github.com/github/awesome-copilot) | Copilot Agent Skills（100+） |
| Vercel | [Vercel AI SDK](https://vercel.com/docs/ai-gateway) | Vercel 平台 skill |
| Google Gemini | [Gemini CLI](https://github.com/google-gemini/gemini-cli) | Gemini CLI 官方 skill |

## 精选 Awesome 列表

| 项目 | Stars | License | 特点 |
|------|-------|---------|------|
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | 23.9K | MIT | 手工精选，含多家官方合作 skill |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | 59.6K | - | 商业/营销分类突出 |
| [libukai/awesome-agent-skills](https://github.com/libukai/awesome-agent-skills) | 4.5K | - | 中英双语，入门指南 |
| [JackyST0/awesome-agent-skills](https://github.com/JackyST0/awesome-agent-skills) | 549 | CC0-1.0 | 中英双语，跨平台安装脚本 |
| [gmh5225/awesome-skills](https://github.com/gmh5225/awesome-skills) | 35 | MIT | 覆盖面最广 |
| [kodustech/awesome-agent-skills](https://github.com/kodustech/awesome-agent-skills) | - | - | 按技术栈分类（前端/后端/DevOps） |
| [FridrichMethod/awesome-skills](https://github.com/FridrichMethod/awesome-skills) | - | - | 1,800+ 自动同步，偏学术 |
| [skillmatic-ai/awesome-agent-skills](https://github.com/skillmatic-ai/awesome-agent-skills) | 236 | - | 渐进式披露深度指南 |
| [EgoAlpha/awesome-DeepAgent-skills](https://github.com/EgoAlpha/awesome-DeepAgent-skills) | - | - | DeepAgent 生态 |

## 技能市场 / 发现平台

| 平台 | 技能数 | 特点 |
|------|--------|------|
| [SkillsMP](https://skillsmp.com) | 1,200,000+ | 最大的市场，自动索引 GitHub |
| [skills.sh](https://skills.sh) | 91,000+ | Vercel 出品，最佳安装体验 |
| [Smithery.ai](https://smithery.ai) | 15,000+ | 显示激活数和 GitHub 星标 |
| [SkillHub.Club](https://skillhub.club) | 16,000+ | AI 质量评分（S/A/B/C） |
| [ClawHub.ai](https://clawhub.ai) | 11,000+ | OpenClaw 技能注册表 |
| [SkillDB](https://github.com/AmazingAng/skilldb) | 180,000+ | 跨平台去重联合索引 |
| [Tencent SkillHub](https://skillhub.tencent.com) | 13,000+ | 腾讯云生态 |
| [AITmpl.com](https://aitmpl.com) | 1,000+ | 一键套件安装 |
| ⭐ **CrazyCodeCat 市场** | 建设中 | 与 CCC 插件原生集成 |

## 按领域分类

### 安全

| Skill | 来源 | Stars | 说明 |
|-------|------|-------|------|
| [trailofbits/skills](https://github.com/trailofbits/skills) | Trail of Bits | - | 安全审计专用 skill |
| CodeQL 分析 | GitHub Copilot | - | 代码安全扫描 |
| OWASP 合规 | GitHub Copilot | - | OWASP 安全规范检查 |

### 前端开发

| Skill | 来源 | 说明 |
|-------|------|------|
| cache-components | Vercel | 组件缓存优化 |
| SVG Animator Pro | SkillsMP | SVG 动画生成 |
| 前端性能优化 | kodustech/awesome | 性能分析 + 优化建议 |
| React Native 技能 | Marshanda14816/agent-skills | React Native 工程化 |

### 后端开发

| Skill | 来源 | 说明 |
|-------|------|------|
| API Tester Pro | SkillsMP | API 测试自动化 |
| LangChain-CR-Pro | 社区 | LangChain 代码审查 |
| Stripe 集成 | VoltAgent | Stripe API 开发 |

### DevOps

| Skill | 来源 | 说明 |
|-------|------|------|
| Cloudflare 部署 | VoltAgent | Cloudflare Workers/Pages 部署 |
| Docker 优化 | 社区 | Dockerfile 最佳实践 |
| CI/CD 配置 | 社区 | GitHub Actions 配置生成 |

### 数据科学 / AI/ML

| Skill | 来源 | 说明 |
|-------|------|------|
| Super Analyst | SkillsMP | 数据分析 |
| Hugging Face 模型 | VoltAgent | HuggingFace 模型集成 |

### 生物信息 / 学术

| Skill | 来源 | 说明 |
|-------|------|------|
| AI4Protein | FridrichMethod | 蛋白质设计 |
| 学术论文写作 | FridrichMethod | 论文格式/引用管理 |
| 科学可视化 | FridrichMethod | 科研图表生成 |

### 法律

| Skill | 来源 | 说明 |
|-------|------|------|
| [CSlawyer1985/claude-for-legal-ZH](https://github.com/CSlawyer1985/claude-for-legal-ZH) | 社区 | 中国法律实务（12 领域，40+ skill） |
| [thuyran/legal-skills-chinese](https://github.com/thuyran/legal-skills-chinese) | 社区 | 中国法律推理/检索（38 个纯 prompt skill） |
| [NEU-ZHA/legal-ai-skills](https://github.com/NEU-ZHA/legal-ai-skills) | 社区 | 法律 AI 技能集（北大法宝 MCP + 引注核验） |
| ⭐ **legal-contract-review** | CCC 市场 | 中国合同审阅 |
| ⭐ **legal-research-assistant** | CCC 市场 | 法律检索辅助 |
| legal-review | LobeHub | 代码库法律合规审查 |

### 营销 / 内容创作

| Skill | 来源 | 说明 |
|-------|------|------|
| [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) | 社区 | 34 个营销 skill，40 万+ 安装量 |
| SEO 优化 | 社区 | 搜索引擎优化建议 |
| 社交媒体管理 | 社区 | 社交平台内容策略 |

### 设计系统（DESIGN.md）

| 资源 | 来源 | 说明 |
|------|------|------|
| [@google/design.md](https://github.com/google-labs-code/design.md) | Google Labs | 官方格式规范 + CLI 工具（lint/diff/export），11K+ ⭐ |
| [awesome-design-md](https://github.com/topics/awesome-design-md) | 社区 | 69+ 品牌模板（Stripe、Vercel、Linear、Notion 等），71K+ ⭐ |
| Stitch MCP | Google Labs | DESIGN.md 的 MCP 服务器集成 |
| `npx @google/design.md lint` | CLI | 校验 DESIGN.md 结构、色彩对比度、token 引用 |

### 游戏开发

| Skill | 来源 | 说明 |
|-------|------|------|
| Unity 技能集 | ClawHub | 431 个 Unity 开发 skill |
| 3D 建模 | 社区 | Blender/Three.js 辅助 |

## 工具与框架

| 工具 | 说明 | 链接 |
|------|------|------|
| [obra/superpowers](https://github.com/obra/superpowers) | 准"标准库"，172K ⭐ | 20+ 高质量 skill |
| [skills.sh CLI](https://skills.sh) | `npx skills add <name>` 一键安装 | Vercel 出品 |
| [CrazyCodeCat 插件](https://github.com/crazycodecat/crazycodecat) | Chrome 扩展，支持 `/skill install/search/update` | 与市场原生集成 |
| [skill-creator](https://claude-plugins.dev/skills/@einverne/dotfiles/skill-creator) | Anthropic 官方 | 创建 skill 的 skill |

## 安全提醒

> **⚠️ 安装第三方 skill 前请务必检查其代码。部分市场上的 skill 未经过安全审核。**

根据调研数据（2026 年中）：
- SkillsMP：1,200,000+ skill，**无安全审核**，约 7% 存在潜在风险
- 建议只安装有 GitHub 星标、最近更新、代码可见的 skill
- CCC 插件的安全扫描（`validateScript`）会在安装时自动检查高危模式

## 贡献

欢迎提交 PR 添加新的 skill 项目或分类。要求：
1. 按现有格式添加到对应分类
2. 注明来源和 License
3. 如果可能，提供 Stars 和说明

---

## License

[MIT](LICENSE)

*部分引用的项目遵循其自身 License。*
