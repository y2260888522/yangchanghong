---
name: "git-push"
description: "Commits all changes and pushes to GitHub remote. Invoke when user asks to commit, push, upload code to GitHub, or save and sync changes."
---

# Git Push 技能

将当前项目的所有变更提交并推送到 GitHub 远程仓库。

## 远程仓库信息
- **URL**: `https://github.com/y2260888522/yangchanghong.git`
- **分支**: `main`
- **认证**: 已配置 SSH 公钥

## 执行步骤

### 1. 检查 git 仓库状态
```
git status
git remote -v
```
如果不是 git 仓库，先执行 `git init`。
如果远程地址不对，执行 `git remote set-url origin https://github.com/y2260888522/yangchanghong.git`。

### 2. 添加所有文件
```
git add .
```

### 3. 提交
```
git commit -m "描述信息"
```
提交信息应简洁描述本次变更内容。

### 4. 推送
```
git branch -M main
git push -u origin main
```

如果是首次推送，使用 `git push -u origin main` 建立跟踪关系；
如果后续推送，直接使用 `git push` 即可。

## 注意事项
- 推送前确认不包含敏感信息（如密码、密钥）
- 大文件请使用 `.gitignore` 排除
- 如果 push 失败（远程有新提交），先执行 `git pull --rebase origin main` 再推送
