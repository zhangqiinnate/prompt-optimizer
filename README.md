# prompt-optimizer

English | [简体中文](README.zh-CN.md)

A [DeepSeek Harness](#requirements) skill that turns a rough prompt into a better one at three intensity levels. It edits the prompt in place, preserves the original intent, and waits for you to choose a level before executing the task.

The skill is invoked as `/prompt-optimizer` and can also be loaded automatically when you ask the model to optimize, polish, or rewrite a prompt.

## What it does

- **L1 — Light fidelity polish**: fixes ambiguity, grammar, pronouns, and redundancy without changing the prompt's structure.
- **L2 — Structured rewrite**: reorganizes the prompt into role, task, context, constraints, output format, and acceptance criteria.
- **L3 — Engineering expansion**: adds deliverables, a step breakdown, edge cases, quality gates, and a self-check list for complex tasks.

The skill does not invent facts, file paths, APIs, or requirements. Unknown details are marked as `<待补充：…>` or `[假设]`, and the optimized prompt keeps the source language.

## Install

### Manual

Download or clone this repository, then copy the folder to your user-level skills directory:

```text
~/.dsh/skills/prompt-optimizer/
```

On Windows:

```text
C:\Users\<you>\.dsh\skills\prompt-optimizer\
```

The resulting layout must be:

```text
~/.dsh/skills/prompt-optimizer/SKILL.md
```

### Git clone

```powershell
git clone https://github.com/<your-name>/prompt-optimizer.git "$env:USERPROFILE\.dsh\skills\prompt-optimizer"
```

If a previous copy exists, move or remove it first, or clone to a temporary folder and copy `SKILL.md` into place.

### Project-level install

To use the skill in one project only, place it here instead:

```text
<project>/.dsh/skills/prompt-optimizer/SKILL.md
```

DSH discovers skills from these roots automatically. Start a new session; if the slash menu does not show the skill, restart DSH once.

## Usage

```text
/prompt-optimizer <your prompt>
/prompt-optimizer 2 <your prompt>
/prompt-optimizer
```

- No level: returns L1, L2, and L3, then waits for your choice.
- `1` / `L1` / `轻` / `轻度`: only L1.
- `2` / `L2` / `标准`: only L2.
- `3` / `L3` / `深` / `深度`: only L3.
- No prompt: optimizes the previous user message.

After the optimized versions appear:

- `用 L2` / `执行 L2`: execute that version.
- `只要 L2` / `只保留稿子`: keep the prompt only, do not execute.
- Or describe the change you want, and the skill revises that level.

You can also skip the slash command and ask “帮我优化这段提示词”; the model can load the skill automatically.

## Levels

| Level | Best for | What changes |
|---|---|---|
| L1 | A basically good prompt that needs clarity | Grammar, ambiguity, pronouns, redundancy; length stays close to the original |
| L2 | Everyday use and most tasks | Full structure: role, task, context, constraints, output format, acceptance criteria |
| L3 | Complex or high-stakes tasks | L2 plus deliverables, step order, edge cases, failure handling, quality gates, self-check |

## Example

Input:

```text
/prompt-optimizer 帮我写个贪吃蛇小游戏
```

Output shape:

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

## Requirements

- DeepSeek Harness with the skills subsystem enabled. The built-in `standard` preset enables it by default.
- No scripts, dependencies, or API keys are required by the skill itself.
- The skill instructions are in Chinese; optimized prompts preserve the source prompt's language.

## Repository layout

```text
prompt-optimizer/
├── SKILL.md
├── README.md
├── README.zh-CN.md
├── LICENSE
└── .gitignore
```

## License

This project is licensed under the [MIT License](LICENSE).

Copyright (c) 2026 prompt-optimizer contributors.
