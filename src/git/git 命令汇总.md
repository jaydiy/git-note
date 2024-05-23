# git 命令汇总

[toc]

## git 常用命令

```bash
# 只克隆最近 1 次 commit
git clone --depth=1 repo_url.git

# example:
# git clone -b release.release-1.0 --depth=1 git@github.com:apache/flink.git

# 添加远程仓库地址
git remote add itwild git@github.com:itwild/flink.git

# 查看远程仓库地址
git remote -v

# 查看远程库与本地分支的信息
git remote show origin

# 将本地当前分支推送到远程 itwild 仓库的 master 分支
git push itwild master

# 强推(需要关闭对分支的保护)，该操作需要谨慎
git push -f itwild master

# 修订上次的提交
git commit --amend

# 修订上次的提交时间
git commit --amend --date="1 minute ago"

# 指定commit时间
git commit --date="10 day ago" -m "Your commit message"

# 调整前几次的提交
git rebase -i HEAD~2

# 从 itwild 远程仓库拉取最新代码(仅仅是拉取代码，并没有参与本地分支merge或者rebase操作)
git fetch itwild

# 展示本地分支的提交历史
git log --graph --pretty=oneline --abbrev-commit


# 展示远程分支itwild/master的提交历史
git log itwild/master

# 可取代merge操作，避免产生不必要的commit，破坏提交树的美观
# 找到两条分支的共同祖先，然后将共同祖先后不同的提交，回放一遍。
git rebase itwild/master

# 本地所有修改的，没有提交的，都返回到原来的状态
# 检出暂存区的代码恢复到工作区
git checkout .

# 把所有没有提交的修改暂存到stash里面。可用git stash pop恢复
git stash

# 返回到某个commit，不保留修改
git reset --hard commit_id

# 返回到某个commit，保留修改
git reset --soft commit_id

```

储藏更改

> git stash 命令是一种在处理紧急任务、切换分支或需要暂时保存当前工作进度时的有力工具。通过理解和正确使用这些命令，可以大大提高工作效率和灵活性

```bash
# 储藏更改:将当前更改的代码储藏起来，等以后恢复使用
git stash

# 命名 stash: 通过添加描述信息，可以更容易地辨别和管理多个 stash
git stash save "修复 bug #42"

# 恢复并删除最近的 stash
git stash pop

# 恢复并删除特定的 stash
git stash pop stash@{n}

# 应用最近一次的 stash，但不删除 stash 记录
git stash apply

# 通过 git stash list，查看本地所有的 stash,如果我要恢复第一个就执行
git stash apply --index 0

# 应用特定的 stash

git stash apply stash@{n}

# 删除最近的 stash
git stash drop

# 删除特定的 stash
git stash drop stash@{n}

# 将 stash 空间清空
git stash clear
```

版本回退

```bash
# 回退至上一个版本
git reset --hard HEAD

# 回退至指定版本
git reset --hard <commit-id>

# 查看以往版本号(本地的commit)
git reflog

# 查看各版本号及信息(所有的commit：本地commit + 其他同事的commit)
git log
```

对已 push 版本进行回退

```bash
# 第一步：本地回退到指定的版本
git reset --hard <commit-id>

# 第二步：将远程的也回退到指定版本
git push origin dev
```

从工作目录中删除所有没有tracked过的文件

```bash
git clean 参数
    -n  Don't actually remove anything, just show what would be done
    -f  --force  If the Git configuration variable clean.requireForce is not set to false, git
     clean will refuse to delete files or directories unless given -f, -n or -i. Git will refuse to delete directories
    with .git sub directory or file unless a second -f is given.
    -d  Remove untracked directories in addition to untracked files

```

cherry-pick某个提交

```bash
git cherry-pick [<options>] <commit-ish>...

常用options:
    --quit                退出当前的chery-pick序列
    --continue            继续当前的chery-pick序列
    --abort               取消当前的chery-pick序列，恢复当前分支
    -n, --no-commit       不自动提交
    -e, --edit            编辑提交信息

```

## git tag

```bash
# 本地打tag
git tag -a release-1.11.2 -m 'Apache Flink 1.11.2' 34372b05(commit版本号)

# 删除一个本地标签
git tag -d <tagname>

# 推送一个本地标签到远程仓库
git push itwild <tagname>

# 推送全部未推送过的本地标签
git push itwild --tags

# 删除一个远程标签
git push itwild :refs/tags/<tagname>

# 查询所有标签
git tag

# 查询标签详细信息
git show v1.0.0
```

## git 配置多个 ssh-key

1. 生成 SSH-Key

   ```bash
   ssh-keygen -t rsa -C "youremail@qq.com" -f "~/.ssh/gitee-rsa"
   ssh-keygen -t rsa -C "youremail@qq.com" -f "~/.ssh/github-rsa"

   ```

1. 把 public key 复制到 gitee 和 github
1. 在 ~/.ssh 目录下新建一个config文件

   ```md
   # gitee
    Host gitee.com
    HostName gitee.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/gitee-rsa

    # github
    Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github-rsa
   ```

1. 测试

   ```bash
   ssh -T git@gitee.com
   ssh -T git@github.com
   ```

## git 代理

- 取消代理

  ```bash
  git config --global --unset http.proxy
  git config --global --unset https.proxy
  ```

- 设置代理

   ```bash
   git config --global http.proxy 'socks5://127.0.0.1:1080'
   git config --global https.proxy 'socks5://127.0.0.1:1080'

   # 仅代理GitHub
   git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
   git config --global --unset http.https://github.com.proxy
   ```

- 111
