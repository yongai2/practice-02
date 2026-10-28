# Git 常用命令笔记

> 本文件在 `dev` 分支上新增，用于演示“在分支上开发新内容”的流程，
> 合并回 `main` 后成为主干内容的一部分。

## 一、仓库级操作

| 命令 | 作用 |
| --- | --- |
| `git clone <URL>` | 把远程仓库完整复制到本地，同时建立 `origin` 远程关联 |
| `git remote -v` | 查看当前仓库关联的远程地址（fetch / push 各一条） |
| `git status` | 查看工作区、暂存区与当前分支的状态 |
| `git log --oneline --graph --decorate` | 以图形化方式查看提交历史与分支走向 |

## 二、提交相关

| 命令 | 作用 |
| --- | --- |
| `git add <文件>` | 把工作区改动放入暂存区（staging area） |
| `git commit -m "<说明>"` | 把暂存区内容生成一次提交，形成版本快照 |
| `git diff` | 查看工作区与暂存区之间的差异 |
| `git checkout -- <文件>` | 丢弃工作区未暂存的修改 |

## 三、分支相关

| 命令 | 作用 |
| --- | --- |
| `git branch` | 列出本地分支，`*` 标记当前所在分支 |
| `git branch -a` | 同时列出本地分支与远程跟踪分支 |
| `git checkout -b dev` | 新建 `dev` 分支并立即切换过去（= branch + checkout） |
| `git merge --no-ff dev` | 把 `dev` 合并进当前分支，并强制保留一条合并提交 |

## 四、远程同步

| 命令 | 作用 |
| --- | --- |
| `git push -u origin main` | 推送 `main` 到远程，并把 `origin/main` 设为上游分支 |
| `git pull --no-rebase origin main` | 拉取远程并合并到本地（保留分叉历史，便于观察冲突） |
| `git fetch origin` | 只下载远程更新，不自动合并 |

## 五、冲突处理三步

1. `git status` 看到 `both modified: <文件>`，说明同一文件的同一区域被双方修改；
2. 打开文件，编辑 `<<<<<<<`、`=======`、`>>>>>>>` 之间的内容，保留最终结果并删除标记；
3. `git add <文件>` 表示冲突已解决，再 `git commit` 完成合并提交。

## 六、一点理解

Git 把“改动”分成三个位置：工作区（改文件的地方）、暂存区（`git add` 后的中转站）、
本地仓库（`git commit` 后的快照）。分支本质上只是一个指向某次提交的可移动指针，
所以创建和切换分支几乎没有成本，这也是 Git 鼓励“小步提交、频繁分支”的原因。

## 七、alice 的补充

- 解决冲突前先用 `git diff` 查看双方差异，避免误删对方内容。
- 解决后用 `git status` 确认出现 “All conflicts fixed but you are still merging”，再执行 `git commit`。
