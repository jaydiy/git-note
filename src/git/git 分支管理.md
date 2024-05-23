## github flow

> github flow 是 git flow 的简化版，专门配合"持续发布"。它是 GitHub 使用的工作流程
>
> 它只有一个长期分支，就是`master`，因此用起来非常简单

- 第一步：根据需求，从master拉出新分支，不区分功能分支或补丁分支
- 第二步：新分支开发完成后，或者需要讨论的时候，就向master发起一个pull request（简称PR）
- 第三步：Pull Request既是一个通知，让别人注意到你的请求，又是一种对话机制，大家一起评审和讨论你的代码。对话过程中，你还可以不断提交代码
- 第四步：你的Pull Request被接受，合并进 master，重新部署后，原来你拉出来的那个分支就被删除。（先部署再合并也可）

## git flow

```md
主分支 master/main

开发分支 dev
  Git 创建 dev 分支的命令：
    git checkout -b dev master
    ## git push -u origin dev
  将 dev 分支发布到 master 分支的命令：
    git checkout master
    git merge --no-ff dev

临时分支：
  功能分支：feature-x
  预发布分支：release
  补丁分支：hotfix

功能分支
  创建一个功能分支：
    git checkout -b feature-x dev
    ## git push -u origin feature-x
  开发完成后，将功能分支合并到 dev 分支：
    ## git pull origin dev
    git checkout dev

    # --no-ff：不使用 fast-forward 方式合并，保留分支的 commit 历史
    # --squash：使用 squash 方式合并，把多次分支 commit 历史压缩为一次
    git merge --no-ff feature-x
    ## git push origin dev
  删除 feature 分支：
    git branch -d feature-x
    ## git push origin :feature-x

预发布分支
  创建一个预发布分支：
    git checkout -b release-0.1.0 dev
  确认没有问题后，合并到 master 分支：
    git checkout master
    git merge --no-ff release-0.1.0
    ## git push
    # 对合并生成的新节点，做一个标签
    git tag -a v1.0.0 -m "第一个版本"
  再合并到 dev 分支：
    git checkout dev
    git merge --no-ff release-0.1.0
    ## git push
  最后，删除预发布分支：
    git branch -d release-0.1.0

补丁分支
  创建一个补丁分支：
    git checkout -b hotfix-0.1 master
  修补结束后，合并到 master 分支：
    git checkout master
    git merge --no-ff hotfix-0.1
    ## git push
    git tag -a v1.1.1 master
    ## git push --tags
  再合并到 dev 分支：
    git checkout dev
    git merge --no-ff hotfix-0.1
  最后，删除"修补bug分支"：
    git branch -d hotfix-0.1
```
