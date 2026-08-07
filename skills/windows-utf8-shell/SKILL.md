---
name: windows-utf8-shell
description: Standardize terminal work on Windows by using PowerShell 7 and explicit UTF-8 initialization. Use automatically whenever the runtime operating system is Windows and a task may execute, generate, or recommend terminal commands, including commands that call external CLIs such as git, rg, or python. Do not use for tasks that do not involve terminal commands or when the runtime is not Windows.
---

# Windows UTF-8 Shell

## Enforce the shell

- Run every terminal command through PowerShell 7 (`pwsh`).
- Permit external CLI programs such as `git`, `rg`, and `python` when launched from PowerShell 7.
- Do not use Windows PowerShell 5.1, `cmd.exe`, Git Bash, WSL, or another shell as the command host.
- If PowerShell 7 is unavailable, stop and report that it is required. Do not silently downgrade.

## Initialize UTF-8

Before running a command that may read, write, or output Chinese or any other non-ASCII content, place this block at the beginning of the same PowerShell process:

```powershell
$utf8NoBom = [System.Text.UTF8Encoding]::new($false)
[Console]::InputEncoding = $utf8NoBom
[Console]::OutputEncoding = $utf8NoBom
$OutputEncoding = $utf8NoBom
$env:PYTHONUTF8 = '1'
$env:PYTHONIOENCODING = 'utf-8'
```

Treat localized command output, non-ASCII paths, text-file content, user-provided text, and commands invoking Python as potentially non-ASCII. When uncertain, initialize UTF-8.

Repeat the initialization block for each independent shell invocation that needs it. Do not assume environment variables, console encodings, profiles, or prior shell state persist across tool calls.

Use explicit UTF-8 options for file and external-tool operations when they provide such options. Do not rely on the Windows system code page, GBK, or a tool's unspecified default encoding.
