## commit message 的规范格式

> IDEA 安装 Git Commit Template 插件

- feat 增加新功能
- fix 修复BUG
- docs 文档/注释
- style 代码风格改变但不影响运行结果(代码格式化、空格和空行调整等)
- refactor 代码重构
- test 测试
- chore 依赖更新/配置更新
- ci 持续集成

```md
# 标题行：50个字符以内，描述主要变更内容
#
# 主体内容：更详细的说明文本，建议72个字符以内。需要描述的信息包括:
#
# * 为什么这个变更是必须的? 它可能是用来修复一个bug，增加一个feature，提升性能、可靠性、稳定性等等
# * 他如何解决这个问题? 具体描述解决问题的步骤
# * 是否存在副作用、风险?
#
# 如果需要的化可以添加一个链接到issue地址或者其它文档
```

## 开发分支规范

```shell
[master] > git checkout develop

[develop] > git add .
[develop] > git commit -m docs(README.md):分支修改项目说明文档
[develop] > git push origin develop
[develop] > git checkout master

[master] > git merge develop
[master] > git add .
[master] > git commit -m sync:主干同步分支
[master] > git push origin master
```
