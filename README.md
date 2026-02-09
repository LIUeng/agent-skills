# Agent Skills

## What

Agent Skills are a lightweight, open format for extending AI agent capabilities with specialized knowledge and workflows.

`技能是一个可移植、支持版本控制的包，用于让 Agent 学会如何执行特定领域的任务。技能既可以包含说明性指令，也可以包含 Agent 可运行的脚本或代码。`

- 可移植

技能适用于任何支持 Agent Skills 标准的 Agent。

- 受版本控制

技能以文件形式存储，可以在你的代码仓库中追踪其变更，或通过 GitHub 仓库链接进行安装。

- 可执行

技能可以包含脚本和代码，由 Agent 执行以完成任务。

- 渐进式

技能按需加载资源，使上下文使用更加高效。

## Usage

| 位置              | 作用域                      |
| ----------------- | --------------------------- |
| .cursor/skills/   | 项目级                      |
| .claude/skills/   | 项目级（兼容 Claude）       |
| .codex/skills/    | 项目级（兼容 Codex）        |
| ~/.cursor/skills/ | 用户级（全局）              |
| ~/.claude/skills/ | 用户级（全局，兼容 Claude） |
| ~/.codex/skills/  | 用户级（全局，兼容 Codex）  |

### Examples

- 每个技能应为一个包含 SKILL.md 文件的文件夹：

```toc
.cursor/
└── skills/
    └── my-skill/
        └── SKILL.md
```

- 技能还可以包含脚本、参考文件和资源等可选目录：

```toc
.cursor/
└── skills/
    └── deploy-app/
        ├── SKILL.md
        ├── scripts/
        │   ├── deploy.sh
        │   └── validate.py
        ├── references/
        │   └── REFERENCE.md
        └── assets/
            └── config-template.json
```

## Support

- Claude
- Cursor IDE
- VSCode IDE
- Trae IDE

## Reference

[Agent Skills](https://agentskills.io/what-are-skills)
[Cursor Skills Usage](https://cursor.com/cn/docs/context/skills)
[Anthropics Skills Templates](https://github.com/anthropics/skills)
