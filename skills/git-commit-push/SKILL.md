---
name: git-commit-push
description: Commit all non-ignored changes in the current Git workspace with a concise English Conventional Commit message after explicit confirmation, then push the current branch to origin. Use when explicitly invoked by the user for committing and pushing all current changes.
---

# Git Commit and Push

Use the following straightforward workflow. The user must explicitly confirm before any commit or push.

## Rules

- Include all tracked modifications, deletions, and non-ignored untracked files: run `git add -A` from the repository root.
- Push only the current branch to `origin/<current-local-branch>`.
- Never force-push, amend, push tags, skip hooks, or bypass repository protection rules.
- Do not automatically run tests, lint, builds, formatting, or other project checks.
- Stop immediately if a Git command fails. Do not attempt risky recovery commands.

## Phase 1: Prepare the confirmation

1. From the repository root, run `git rev-parse --show-toplevel` to confirm the current directory is a Git worktree.
2. Get the current branch with `git branch --show-current`. Stop if `HEAD` is detached or the branch is `main` or `master`.
3. Confirm that a remote named `origin` exists. Do not substitute another remote.
4. Confirm `user.name` and `user.email` are configured with `git config --get`. Stop and identify the missing item if either is absent.
5. Run `git status --short`. Stop if it shows no changes.
6. Propose a concise English Conventional Commit message:
   - Use one of `feat`, `fix`, `refactor`, `docs`, `test`, `build`, `ci`, or `chore`.
   - Use `type(scope): English summary` only when there is one clear scope; otherwise use `type: English summary`.
   - Use an ASCII colon followed by a space. Do not add a trailing period or body unless the user requests one.
7. Show this confirmation table:

| 项目 | 内容 |
|---|---|
| 当前分支 | `<current-local-branch>` |
| 推送目标 | `origin/<current-local-branch>` |
| 提交信息 | `<proposed-commit-message>` |
| 改动状态 | `<git-status-short-output>` |
| 项目检查 | 未运行项目测试、lint 或构建。 |

Then ask exactly once: `是否继续提交并推送？请输入是或否。`

End the turn and wait for the user's reply. Continue only when the trimmed answer is exactly `是`. Treat `否`, any other text, an empty reply, or ambiguous agreement as rejection; state that nothing was staged, committed, or pushed, then stop.

## Phase 2: Commit and push

Only after receiving the exact answer `是`:

1. Re-check that the repository, current branch, and `origin` are still available.
2. From the repository root, run `git add -A`.
3. Verify that there is a staged change with `git diff --cached --quiet`; stop if there is none.
4. Create one commit using normal hooks and the approved message.
5. If commit creation fails, stop and report the failure; do not push.
6. Push with `git push -u origin <current-local-branch>`.
7. If push fails, keep the local commit, report the error and commit ID, and do not roll back or force-push.
8. On success, report the new commit ID, commit title, current branch, and `origin/<branch>` target.

## Required stop behavior

Before confirmation, do not change the real index, commit history, or remote. If a local commit succeeds but cannot be pushed, state clearly that it exists only locally.
