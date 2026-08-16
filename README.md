# AI Skills

**English** | [简体中文](README.zh-CN.md)

A collection of reusable skills for AI coding agents. Each skill packages focused instructions and workflows in the open `SKILL.md` format so supported agents can discover and apply them consistently.

## Available skills

| Skill | Description |
| --- | --- |
| [`git-commit-push`](skills/git-commit-push/) | Safely stages all intended changes, proposes a concise English Conventional Commit message, asks for explicit confirmation, and pushes the current branch to `origin`. |
| [`windows-utf8-shell`](skills/windows-utf8-shell/) | Standardizes Windows terminal work on PowerShell 7 with explicit UTF-8 initialization for non-ASCII input, output, and file operations. |

## Requirements

- [Node.js](https://nodejs.org/) with `pnpm`
- A supported AI coding agent, such as [Codex](https://developers.openai.com/codex/skills)

## Install with the skills CLI

This repository follows the [`skills/<name>/SKILL.md`](https://github.com/vercel-labs/skills) discovery layout and can be installed through the [skills.sh](https://skills.sh/) CLI.

Start the interactive installer and choose the skills you want to install:

pnpm dlx skills add limi58/skills
```

Start a new Codex session after installation so the newly installed skills are discovered.

Compatibility with the skills CLI means these skills can be installed from this repository. It does not imply official listing, verification, certification, or endorsement by skills.sh.

## Update installed skills

Update installed skills interactively:

```shell
pnpm dlx skills update
```

Update a specific skill:

```shell
pnpm dlx skills update windows-utf8-shell
```

## License

Released under the [MIT License](LICENSE).
