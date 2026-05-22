# AI Content Critic

一个用于识别 AI 生成内容问题的尖锐但有有理有据的审稿 Skill：发现文章、图片、PPT、海报和 UI 里的 AI 味，并转化成具体修改方案。

AI Content Critic 是一个同时面向 Claude Code 和 Codex 的跨 Agent Skill，用来审查 AI 生成的文章、图片、PPT、海报、UI 截图以及图文混合内容。

它不是一个“AI 检测器”，也不会证明作者身份。它诊断的是一组质量信号：哪些地方显得合成感强、空泛、套路化、不可信、不美观，或者不适合真实发布。

## 它能做什么

- 发现文章、论文段落、报告、社媒文案、营销文案里的 AI 味
- 指出套话、空话、逻辑薄弱、伪具体、重复结构和缺少证据的问题
- 检查 AI 生成图片中的手部、面部、文字、光影、透视、材质、边缘和场景一致性问题
- 检查 PPT、海报和 UI 截图中的信息层级、版式密度、字号、对齐、视觉证据和模板感
- 支持多种审稿语气：温和、直接、吐槽、导师式、客户审稿式
- 基于可观察证据做判断，不会随便宣称某个内容“绝对是 AI 生成”

## 快速开始

根据你使用的 Agent 安装。

### Claude Code

项目内安装：

```bash
mkdir -p .claude/skills
cp -R skills/ai-content-critic .claude/skills/
```

个人全局安装：

```bash
mkdir -p ~/.claude/skills
cp -R skills/ai-content-critic ~/.claude/skills/
```

然后在 Claude Code 中使用：

```text
/ai-content-critic 帮我锐评这张 AI 生成海报，别客气
```

Claude Code 的 Skill 本质上是文件系统中的 `SKILL.md` 文件。项目级 Skill 放在 `.claude/skills/<name>/SKILL.md`，个人级 Skill 放在 `~/.claude/skills/<name>/SKILL.md`。

### Codex

个人全局安装：

```bash
mkdir -p ~/.codex/skills
cp -R skills/ai-content-critic ~/.codex/skills/
```

如果你把这个仓库发布为 Codex 插件，`codex-plugin/plugin.json` 已经指向了 `./skills/` 目录。

然后在 Codex 中使用：

```text
Use $ai-content-critic to roast this AI-generated article and give me a rewrite plan.
```

也可以直接中文提问：

```text
使用 $ai-content-critic 帮我吐槽这篇 AI 写的文章，并给出修改方案。
```

## 验证安装

安装后，开启一个新的 Agent 会话并询问：

```text
What skills are available?
```

也可以直接测试：

```text
使用 ai-content-critic 审查这句话：“在当今快速发展的时代，创新比以往任何时候都更加重要。”
```
Agent 应该能识别 `ai-content-critic`，或者直接给出符合“总体判断、问题、原因、修改建议”结构的审稿输出。

如果 Skill 没有被识别：

- 确认仓库中存在 `skills/ai-content-critic/SKILL.md`。
- Claude Code 项目级安装时，确认文件位于 `.claude/skills/ai-content-critic/SKILL.md`。
- Claude Code 个人级安装时，确认文件位于 `~/.claude/skills/ai-content-critic/SKILL.md`。
- Codex 个人级安装时，确认文件位于 `~/.codex/skills/ai-content-critic/SKILL.md`。
- 如果会话启动时 skill 目录还不存在，重启 Agent 会话。
- 如果按插件方式安装，确认 `codex-plugin/plugin.json` 或 `claude-plugin/plugin.json` 已进入仓库，并且 manifest 指向 `./skills/`。

## 示例提示词

```text
使用 ai-content-critic 审查这篇文章，告诉我哪些地方像 AI 写的，哪些内容应该删掉。
```

```text
使用 ai-content-critic 看这张图。先吐槽，再给我修图或重新生成的建议。
```

```text
使用 ai-content-critic 检查这套 PPT，重点看 AI 味、信息层级和字号可读性。
```

```text
使用 ai-content-critic 的客户审稿模式。不要开玩笑，只列问题和修改建议。
```

```text
帮我锐评这个海报：哪里廉价、哪里像模板、哪里一看就是 AI 糊出来的？
```

更多输出样例见 `examples/` 目录：

- `examples/text-review.md`
- `examples/image-review.md`
- `examples/slide-review.md`
- `examples/roast-mode.md`
- `examples/client-ready-mode.md`

## 输出风格

这个 Skill 通常会输出：

1. 一句话总体判断
2. 按严重程度排序的问题列表
3. 为什么这些问题会让内容显得 AI 味重或质量低
4. 具体修改建议、重写方向、修图方案或重新生成提示词方向

当用户说“吐槽”“锐评”“毒舌”“别客气”或 “roast” 时，诊断部分会更尖锐、更有梗，但修改建议仍然保持具体、可执行。

## 适合检查的内容

### 文本

- AI 写作腔
- 套话堆叠
- 逻辑跳跃
- 缺少例子和证据
- 伪专业、假深刻
- 中英文语气不自然
- 标题和正文不匹配

### 图片

- 手、脸、身体结构异常
- 文字乱码或变形
- 光影和透视不一致
- 材质塑料感或糊成一团
- 边缘、纹理、重复图案异常
- 场景元素互相矛盾
- 构图没有重点

### PPT、海报和 UI

- 字号太小
- 文本太多
- 图表不可读
- 层级混乱
- 对齐漂移
- 图像只是装饰，没有承担论证作用
- 模板感、廉价感、AI 自动生成感太强

## 仓库结构

```text
.
├── claude-plugin/
│   └── plugin.json
├── codex-plugin/
│   └── plugin.json
├── examples/
│   ├── client-ready-mode.md
│   ├── image-review.md
│   ├── roast-mode.md
│   ├── slide-review.md
│   └── text-review.md
├── skills/
│   └── ai-content-critic/
│       └── SKILL.md
├── AGENTS.md
├── CLAUDE.md
├── LICENSE
├── README.md
├── README.zh-CN.md
└── package.json
```

## 设计原则

- 证据优先，不靠感觉乱判
- 先指出真正影响质量的问题
- 批评内容，不攻击创作者
- “像 AI 生成”是一组质量信号，不是来源证明
- 可以幽默吐槽，但不能胡说
- 每个主要问题都要给出可执行修改方案


## 许可证

MIT License。详见 `LICENSE`。
