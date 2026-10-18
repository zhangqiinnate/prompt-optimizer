# prompt-optimizer

[English](README.md) | 简体中文

一个 DeepSeek Harness 技能：把粗糙的提示词就地优化成更好的版本，提供三种强度。它只改提示词本身，保留原始意图，并在执行任务前等待你选择档位。

通过 `/prompt-optimizer` 调用；当你直接说“帮我优化/润色/改写这段提示词”时，模型也可以自动加载它。

## 功能

- **L1 轻度·保真**：修歧义、病句、指代和冗余，不改变原提示词结构。
- **L2 标准·结构化**：重组为角色、任务、上下文、约束、输出格式和验收标准。
- **L3 深度·工程化**：面向复杂任务，增加交付物、步骤拆解、边界情况、质量门槛和自检清单。

技能不会虚构事实、文件路径、API 或需求。未知信息用 `<待补充：…>` 或 `[假设]` 标注；优化稿保持源提示词的语言。

## 安装

### 手动安装

下载或克隆本仓库，然后把整个目录复制到用户级技能目录：

```text
~/.dsh/skills/prompt-optimizer/
```

Windows：

```text
C:\Users\<你>\.dsh\skills\prompt-optimizer\
```

最终结构必须包含：

```text
~/.dsh/skills/prompt-optimizer/SKILL.md
```

### 使用 git clone

```powershell
git clone https://github.com/<你的用户名>/prompt-optimizer.git "$env:USERPROFILE\.dsh\skills\prompt-optimizer"
```

如果已经安装过旧版本，先移动或删除旧目录，或者克隆到临时目录后把 `SKILL.md` 复制进去。

### 项目级安装

只在一个项目中使用时，放到：

```text
<项目>/.dsh/skills/prompt-optimizer/SKILL.md
```

DSH 会自动发现这些目录中的技能。新开一个会话即可；如果斜杠菜单没有显示，重启一次 DSH。

## 用法

```text
/prompt-optimizer <你的提示词>
/prompt-optimizer 2 <你的提示词>
/prompt-optimizer
```

- 不带档位：输出 L1、L2、L3 三档，然后等待选择。
- `1` / `L1` / `轻` / `轻度`：只输出 L1。
- `2` / `L2` / `标准`：只输出 L2。
- `3` / `L3` / `深` / `深度`：只输出 L3。
- 不带提示词：优化上一条用户消息。

看到优化稿后：

- `用 L2` / `执行 L2`：按该版本执行任务。
- `只要 L2` / `只保留稿子`：只保留提示词，不执行。
- 也可以直接说明想怎么改，技能只会修改对应档位。

也可以不打斜杠命令，直接说“帮我优化这段提示词”，模型可以自动加载技能。

## 三档说明

| 档位 | 适合 | 主要变化 |
|---|---|---|
| L1 | 本身不错、只需要说清楚的提示词 | 修语法、歧义、指代和冗余；长度接近原文 |
| L2 | 日常使用和大多数任务 | 补全角色、任务、上下文、约束、输出格式、验收标准 |
| L3 | 复杂或高风险任务 | 在 L2 基础上增加交付物、步骤顺序、边界情况、失败处理、质量门槛和自检 |

## 示例

输入：

```text
/prompt-optimizer 帮我写个贪吃蛇小游戏
```

输出结构：

```text
**诊断**：...

### L1 · 轻度（保真）
...

### L2 · 标准（结构化，推荐）
...

### L3 · 深度（工程化）
...

回复「用 L1 / L2 / L3」执行对应版本；回复「只要 L2」只保留稿子；也可以直接说怎么改。
```

## 环境要求

- DeepSeek Harness，并启用技能子系统。内置的 `standard` 预设默认启用。
- 技能本身不需要脚本、依赖或 API Key。
- 技能说明使用中文；优化稿保持源提示词的语言。

## 仓库结构

```text
prompt-optimizer/
├── SKILL.md
├── README.md
├── README.zh-CN.md
├── LICENSE
└── .gitignore
```

## 许可证

本项目使用 [MIT License](LICENSE)。

Copyright (c) 2026 prompt-optimizer contributors.
