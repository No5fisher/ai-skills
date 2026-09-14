# 中餐烹饪领域知识框架 · 迁移安装包

> 技能名：`chinese-cuisine-framework`
> 来源：`~/.openclaw/workspace/skills/chinese-cuisine-framework/`（2026-09-13 导出）
> 体积：276 KB ／ 10 个文件 ／ **纯文本，零外部依赖**
> 打包时间：2026-09-13 21:45 PDT

---

## 1. 包里有什么

```
chinese-cuisine-framework/
├── SKILL.md                              40 KB  ← 技能本体（含 frontmatter）
└── references/
    ├── refine-a.md                       11 KB
    ├── refine-b.md                       14 KB
    ├── validation.md                      7 KB
    └── research/
        ├── 01-science.md                 26 KB  科学原理
        ├── 02-techniques.md              36 KB  技法
        ├── 03-flavor.md                  33 KB  调味
        ├── 04-ingredients.md             32 KB  食材
        ├── 05-cuisine-schools.md         36 KB  菜系流派
        └── 06-literature.md              30 KB  文献出处
```

- `SKILL.md` 是主体：框架概览 / 回答工作流 / 心智模型 / 决策启发式 / 流派对比 / 技法速查 / 调味逻辑 / 食材处理 / 诚实边界。
- `references/` 是调研底稿（含逐条可信度分级与未核验标注）。SKILL.md 第 339 行指向 `references/research/01–06`。
- **`references/` 是附录，不是运行必需**：只装 `SKILL.md` 也能正常工作，只是少了溯源细节。

---

## 2. 兼容性（已验证）

| 检查项 | 结果 |
|---|---|
| frontmatter 格式 | `name` + `description` 两个字段，标准 Agent Skills 规范 |
| description 长度 | 490 字符（规范上限 1024）✔ |
| 绝对路径 | 无（`grep /Users/ ~/ /opt/` 全部为空）✔ |
| 外部依赖 | 无脚本、无二进制、无网络调用、无 pip/npm 依赖 ✔ |
| 机器绑定 | 无（不含主机名、端口、密钥）✔ |
| 内部引用 | 仅一处相对路径 `references/research/01–06`，**保持目录结构即可** |

**结论：可直接搬到任何支持 skills 的 AI 环境，无需改造。**

---

## 3. 安装位置

### OpenClaw
```bash
# 方式 A：只给 main agent（推荐）
mkdir -p ~/.openclaw/workspace/skills
unzip chinese-cuisine-framework.zip -d ~/.openclaw/workspace/skills/

# 方式 B：跨 agent / 跨项目共享
unzip chinese-cuisine-framework.zip -d ~/.agents/skills/

# 验证
openclaw skills list | grep chinese-cuisine
```
> 技能按会话加载，通常无需重启 Gateway。

### Claude Code / Claude Desktop（Agent Skills）
```bash
mkdir -p ~/.claude/skills
unzip chinese-cuisine-framework.zip -d ~/.claude/skills/
```
> 项目级安装放 `<项目根>/.claude/skills/`。

### 其它 AI / 通用做法
- 若支持"技能目录"约定：把 `chinese-cuisine-framework/`（**整个文件夹**）放进它约定的 skills 目录。
- 若只支持"自定义指令 / 知识库上传"：上传 `SKILL.md`，把 `references/` 一并作为知识库文件（或按需再上传）。
- 若只支持粘贴文本：把 `SKILL.md` 正文粘进系统提示（约 40 KB）；`references/` 太大，按需取用。

⚠️ **一定保持文件夹结构。** 把 10 个文件平铺到一个目录会破坏 `references/` 的相对引用。

---

## 4. 装完怎么验

```bash
# 1) 文件齐不齐（应为 10）
find chinese-cuisine-framework -type f | wc -l

# 2) frontmatter 可解析
python3 - <<'PY'
import re,yaml
t=open("chinese-cuisine-framework/SKILL.md",encoding="utf-8").read()
fm=re.match(r"^---\n(.*?)\n---\n",t,re.S).group(1)
y=yaml.safe_load(fm)
assert y["name"]=="chinese-cuisine-framework"
print("OK  name:",y["name"],"| description:",len(y["description"]),"字符")
PY

# 3) 无绝对路径
grep -rn -E "/Users/|~/\.|/opt/" chinese-cuisine-framework/ || echo "OK  无绝对路径"

# 4) 校验和
shasum -a 256 -c SHA256SUMS.txt
```

**功能自测（装好后问一句即可）**：
> 「为什么我炒的肉总是发柴？」

预期：不直接给菜谱，而是先翻译成"嫩肉在高温快炒中脱水"的机制问题，调「水分即口感 + 火候即能量管理」两个模型，
给出温度/时间/现象级判据，并在末尾区分"事实 / 框架推断 / 未经核验"。

---

## 5. 行为要点（避免误用）

- **会激活**：做法求助、原理好奇（为什么发柴/粘锅/吸油/不绿）、判断咨询（油温够了吗 / 该炒还是炖 / 镬气）、菜系比较、与中餐技法相关的健康话题。
- **不激活（防呆）**：餐馆推荐、点菜、外卖、价格等消费场景；非中餐烹饪；闲聊寒暄。
- **健康话题立场**：只并列双方证据与监管共识，明示"不构成膳食建议"，不站队。
- **不调和矛盾**：菜系正宗、技法流派的分歧并列呈现，由使用者自决。
- **表达风格**：给温度/时间/现象，不用"少许""适量"糊弄；不玄学化；不拟人、不模仿人物语气。

---

## 6. 附：SHA256

见同目录 `SHA256SUMS.txt`。跨设备传输后建议先校验再安装。
