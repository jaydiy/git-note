# 这是一个学习 git 的笔记

## 创建项目

1. 新建项目

   ```bash
   npm iniy -y
   git init
   ```

1. `.gitignore`

   ```bash
   node_modules
   dist
   package-lock.json
   !.vscode/extensions.json
   ```

1. 1

## 提交规范

1. 安装 Commitizen CLI 工具

   ```bash
   npm install -g commitizen
   ```

1. 在项目目录里，初始化项目以使用 cz-conventional-changelog 适配器

   ```bash
   commitizen init cz-conventional-changelog --save --save-exact
   # 主要做了以下三件事
   #   1. 安装cz-conventional-changelog（适配器）的npm包
   #   2. 将其保存到 package.json 的 devDependency
   #   3. 在 package.json 中添加 config.commitizen 
   ```

1. 提交代码 `git add. & git cz`

   也可以在 `package.json`中添加脚本，运行 `npm run cz` 提交代码

   ```json
    // package.json
    "scripts": {
       "cz": "git-cz"
    } 
   ```
