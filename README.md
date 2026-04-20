# Claude Code MBTI 插件

<p align="center">
  <b>中文</b> · <a href="README.en.md">English</a>
</p>

<p align="center">
  <img src="examples/intj.png" alt="INTJ — 建筑师" width="240" />
</p>

一个 Claude Code 插件，把 16 种 MBTI 人格打包成 16 个 skill。一行斜杠命令，切换 Claude 说话的方式。

```
/mbti:intj    帮我想想这次迁移的策略
/mbti:enfp    帮我重写这个落地页
/mbti:istp    这个脚本到底哪儿错了
```

每个 skill 只改变 **语气、风格、思考习惯、决策默认值**，不会改 Claude 的工具、权限或安全行为。

去爹味用 `/mbti:intj`，做设计用 `/mbti:enfp`，调 bug 用 `/mbti:istp`。

## 安装

### 方式 A —— 从 marketplace 安装（推荐）

在 Claude Code 里一次性添加 marketplace，然后安装：

```
/plugin marketplace add guoriyue/mbti-skills
/plugin install mbti@mbti-skills
/reload-plugins
```

之后更新：

```
/plugin marketplace update mbti-skills
/plugin update mbti@mbti-skills
/reload-plugins
```

### 方式 B —— 本地源码安装（开发者）

克隆仓库，用插件启动 Claude Code：

```bash
git clone https://github.com/guoriyue/mbti-skills.git ~/.claude/plugins/mbti-skills
claude --plugin-dir ~/.claude/plugins/mbti-skills
```

在会话里运行 `/reload-plugins` 可以不重启直接热加载，方便调试。

## 使用

任意人格通过 `/mbti:<类型>` 调用：

```
/mbti:intj
/mbti:enfp
/mbti:istp
```

人格会持续整个对话。想换就再调一个类型，或者直接说"去掉这个人格"回到默认 Claude。

## 16 种人格

### 分析师（NT）
| 命令 | 类型 | 别称 | 适合 |
|---|---|---|---|
| `/mbti:intj` | INTJ | 建筑师 | 长期战略、系统级思考 |
| `/mbti:intp` | INTP | 逻辑学家 | 第一性原理推导、理论探索 |
| `/mbti:entj` | ENTJ | 指挥官 | 果断决策、执行规划 |
| `/mbti:entp` | ENTP | 辩论家 | 头脑风暴、唱反调 |

### 外交官（NF）
| 命令 | 类型 | 别称 | 适合 |
|---|---|---|---|
| `/mbti:infj` | INFJ | 提倡者 | 反思性、价值观对齐的建议 |
| `/mbti:infp` | INFP | 调停者 | 温和、聚焦意义的支持 |
| `/mbti:enfj` | ENFJ | 主人公 | 辅导式、有结构的鼓励 |
| `/mbti:enfp` | ENFP | 竞选者 | 好玩的脑暴、创意能量 |

### 守护者（SJ）
| 命令 | 类型 | 别称 | 适合 |
|---|---|---|---|
| `/mbti:istj` | ISTJ | 物流师 | 严谨、按规矩执行 |
| `/mbti:isfj` | ISFJ | 守卫者 | 耐心、细致、有保护欲的支持 |
| `/mbti:estj` | ESTJ | 总经理 | 组织化、讲结果的执行 |
| `/mbti:esfj` | ESFJ | 执政官 | 温暖、兼顾人际的协作 |

### 探险家（SP）
| 命令 | 类型 | 别称 | 适合 |
|---|---|---|---|
| `/mbti:istp` | ISTP | 鉴赏家 | 动手调 bug、话少信号高 |
| `/mbti:isfp` | ISFP | 探险家 | 审美取向、低压力的手艺活 |
| `/mbti:estp` | ESTP | 企业家 | 快速、务实、先动手再说 |
| `/mbti:esfp` | ESFP | 表演者 | 乐观、具体、推进节奏 |

## 示例

### 写代码 —— debug 一次 RL 训练

同样的问题、同样的日志。默认 Claude 面面俱到；INTJ 直接给诊断和行动顺序。

| Base | `/mbti:intj` |
|---|---|
| ![默认 Claude 回答 RL debug 问题](examples/coding-base.png) | ![INTJ 回答同一个问题](examples/coding-intj-on.png) |

### 前端 —— 同一个 prompt 写落地页

Prompt：*"给一个叫 Marginal 的 AI 笔记 app 写落地页。"* 默认 Claude 出的是干净保守的版本；`/mbti:enfp` 出的是好玩、鲜艳、大声的版本。

| Base | `/mbti:enfp` |
|---|---|
| ![默认 Claude 的 Marginal 落地页](examples/frontend-base.png) | ![ENFP Claude 的 Marginal 落地页](examples/frontend-enfp.png) |

源码：[`examples/frontend-base.html`](examples/frontend-base.html) · [`examples/frontend-enfp.html`](examples/frontend-enfp.html)

## 目录结构

```
.claude-plugin/
  plugin.json          ← 插件清单（name: "mbti"）
skills/
  intj/SKILL.md
  intp/SKILL.md
  entj/SKILL.md
  ...                  ← 共 16 个
README.md
```

`plugin.json` 里的插件名 `mbti`，决定了 `intj/` 这个 skill 文件夹变成斜杠命令 `/mbti:intj`。

每个 `SKILL.md` 有 YAML frontmatter（`name`、`description`）和四个部分：

- **Voice and style** —— 怎么说话
- **How to think** —— 关注什么、强调什么
- **How to decide** —— 选项之间如何默认取舍
- **Avoid** —— 这个类型容易走偏的地方，避免自我漫画化

## 自定义

这些只是起点，不是定论。改任意 `SKILL.md` 调成你想要的声音，再 `/reload-plugins` 热加载，不用重启。

推荐第一个改动：在 **Voice and style** 里加一行，指名某个人的说话风格让 Claude 模仿。

## 声明

MBTI 是一种松散的分类学，不是严谨的人格科学。这些 skill 是为了好玩，不要用来给自己、同事或模型下结论。
