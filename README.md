# AI Skills

个人 AI 技能集（Agent Skills 规范）。每个技能一个顶层目录，可独立安装。

## 技能索引

| 技能 | 说明 | 安装 |
|---|---|---|
| [chinese-cuisine-framework](chinese-cuisine-framework/) | 中餐烹饪领域知识框架 —— 以火候/调味/刀工/食材四支柱 + 菜系坐标系构成的决策框架，让 AI 从原理推断做法而非背菜谱 | `unzip chinese-cuisine-framework.zip -d <skills 目录>` 或直接复制目录；详见 [INSTALL.md](INSTALL.md) |

---

## chinese-cuisine-framework

### 它解决什么问题

问「红烧肉怎么做」，多数 AI 给你一份菜谱。装上这个技能后，它会：

- **先分类再回答**：菜谱请求 / 原理提问 / 判断咨询 / 健康安全 / 替代咨询，五类走不同路径
- **给机制而不是口诀**：把「为什么上浆」翻译成「如何防止嫩肉在高温快炒中脱水」，给出温度、时间、可观察现象
- **三分标注**：事实（带调研出处）/ 框架推断 / 未经核验，明说哪条没核实过
- **不调和矛盾**：菜系正宗、技法流派的分歧并列呈现，由使用者自决
- **健康话题只并列证据**，不给膳食建议、不站队

### 安装

```bash
git clone https://github.com/<owner>/<repo>.git
cd <repo>

# OpenClaw（单 agent）
unzip chinese-cuisine-framework.zip -d ~/.openclaw/workspace/skills/

# OpenClaw（跨 agent 共享）
unzip chinese-cuisine-framework.zip -d ~/.agents/skills/

# Claude Code / Claude Desktop
unzip chinese-cuisine-framework.zip -d ~/.claude/skills/
```

或直接把 `chinese-cuisine-framework/` 整个文件夹复制到目标环境的 skills 目录。

> ⚠️ **保持文件夹结构**。SKILL.md 用相对路径引用 `references/research/01–06`，平铺文件会破坏引用。

### 结构

```
chinese-cuisine-framework/
├── SKILL.md                    40 KB  ← 技能本体
└── references/
    ├── refine-a.md             11 KB
    ├── refine-b.md             14 KB
    ├── validation.md            7 KB
    └── research/
        ├── 01-science.md       26 KB  科学原理
        ├── 02-techniques.md    36 KB  技法
        ├── 03-flavor.md        33 KB  调味
        ├── 04-ingredients.md   32 KB  食材
        ├── 05-cuisine-schools.md 36 KB  菜系流派
        └── 06-literature.md    30 KB  文献出处
```

- `SKILL.md` 十节：框架概览 / 回答工作流 / 心智模型 / 决策启发式 / 流派对比 / 技法速查 / 调味逻辑 / 食材处理 / 诚实边界 / 调研来源
- `references/` 是调研底稿，含逐条可信度分级与未核验标注。**是附录，不是运行必需** —— 只装 `SKILL.md` 也能工作

### 兼容性

| 检查项 | 结果 |
|---|---|
| frontmatter | 标准 Agent Skills 规范：`name` + `description` |
| description 长度 | 490 字符（规范上限 1024） |
| 绝对路径 | 无 |
| 外部依赖 | 无（纯文本，无脚本/二进制/网络调用） |

### 行为边界

- **会激活**：做法求助、原理好奇（为什么发柴/粘锅/吸油/不绿）、判断咨询（油温够了吗 / 该炒还是炖 / 镬气）、菜系比较、与技法相关的健康话题
- **不激活（防呆）**：餐馆推荐、点菜、外卖、价格等消费场景；非中餐烹饪；闲聊
- **不玄学化**：「镬气」必须给化学解释
- **不拟人**：不模仿任何人物语气

### 校验

```bash
shasum -a 256 -c SHA256SUMS.txt
```

安装细节见 [INSTALL.md](INSTALL.md)。
