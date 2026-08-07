# AI Skills

[English](README.md) | **简体中文**

面向 AI 编程代理的可复用 Skills 集合。每个 skill 都使用开放的 `SKILL.md` 格式封装专门的指令和工作流，使受支持的代理能够稳定地发现并应用它们。

## 可用 Skills

| Skill | 说明 |
| --- | --- |
| [`git-commit-push`](skills/git-commit-push/) | 安全暂存预期改动，生成简洁的英文 Conventional Commit 信息，在获得明确确认后将当前分支推送到 `origin`。 |
| [`windows-utf8-shell`](skills/windows-utf8-shell/) | 在 Windows 中统一使用 PowerShell 7，并为非 ASCII 输入、输出和文件操作显式初始化 UTF-8。 |

## 环境要求

- 带有 `npm` 和 `npx` 的 [Node.js](https://nodejs.org/)
- 受支持的 AI 编程代理，例如 [Codex](https://developers.openai.com/codex/skills)

## 使用 skills CLI 安装

本仓库遵循 [`skills/<name>/SKILL.md`](https://github.com/vercel-labs/skills) 发现结构，可通过 [skills.sh](https://skills.sh/) CLI 安装。

列出可用的 skills：

```powershell
npx skills add limi58/skills --list
```

启动交互式安装器：

```powershell
npx skills add limi58/skills
```

安装指定 skill：

```powershell
npx skills add limi58/skills --skill git-commit-push
npx skills add limi58/skills --skill windows-utf8-shell
```

在当前项目中为 Codex 安装整个集合：

```powershell
npx skills add limi58/skills -a codex
```

为 Codex 全局安装整个集合：

```powershell
npx skills add limi58/skills -g -a codex
```

安装后请启动新的 Codex 会话，使新安装的 skills 被正确发现。

兼容 skills CLI 仅表示这些 skills 可以从本仓库安装，不代表获得 skills.sh 的官方收录、验证、认证或背书。

## 更新已安装的 skills

交互式更新已安装的 skills：

```powershell
npx skills update
```

更新指定 skill：

```powershell
npx skills update windows-utf8-shell
```

## 许可证

本项目使用 [MIT License](LICENSE)。
