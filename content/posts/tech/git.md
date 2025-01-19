---
title: 'Git'
date: 2025-01-18
tags: ['技术', 'git']
---

[**_`官方文档`_**](https://git-scm.com/book/zh/v2)

# 裸仓库

[服务器上的 Git](https://git-scm.com/book/zh/v2/服务器上的-Git-协议)

> 设置默认分支为 `main`

```
PS D:\> git config --global init.defaultBranch main
```

> 初始一个测试仓库 `test.git`

```
PS D:\data\git\repo> git init --bare test.git

```

> 测试

```
PS D:\data\git\repo> git clone D:/data/git/repo/test.git D:/data/git/repo/test
Cloning into 'D:/data/git/repo/test'...
warning: You appear to have cloned an empty repository.
done.
PS D:\data\git\repo> cd .\test\
PS D:\data\git\repo\test> ls
PS D:\data\git\repo\test> echo "Hello, Git" > file.txt
PS D:\data\git\repo\test> git add file.txt
PS D:\data\git\repo\test> git commit -m "Add file.txt"
[main (root-commit) ac38950] Add file.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file.txt
PS D:\data\git\repo\test> git push
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 240 bytes | 240.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To D:/data/git/repo/test.git
 * [new branch]      main -> main
PS D:\data\git\repo\test>
```

# 使用

## tag

[2.6 打标签](https://git-scm.com/book/zh/v2/Git-基础-打标签)

> 轻量级标签（Lightweight Tag）

这会使用当前的提交信息，直接跳过编辑过程，只修改提交信息。

```
git tag v1.0.0

```

> 注释标签（Annotated Tag）

注释标签包含更多信息，例如标签的作者和日期。一般推荐使用注释标签。

```
git tag -a v1.0.0 -m "v1.0.0 版本信息"

```

> 删除

```
git tag -d v1.0.0
```

这将会删除本地的 `v1.0.0` 标签，但不会影响远程仓库。

> 推送

```
# 推送一个
git push origin v1.0.0

# 推送所有
git push --tags
```

## 未 push 的 commit 信息修改

[2.4 撤消操作](https://git-scm.com/book/zh/v2/Git-基础-撤消操作)
[7.6 重写历史](https://git-scm.com/book/zh/v2/Git-工具-重写历史)

> 1. 修改最后一次的提交信息

```
git commit --amend
```

这会打开你设置的默认文本编辑器，允许你修改提交信息。修改后，保存并关闭编辑器即可。

> 2.修改提交信息但保持文件不变

```
git commit --amend --no-edit
```

这会使用当前的提交信息，直接跳过编辑过程，只修改提交信息。
