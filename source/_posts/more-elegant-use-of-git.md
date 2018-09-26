---
title: 更优雅的使用 Git
date: 2018-05-08
---

## 写好 commit message

Git 每次提交代码，都要写 Commit message，否则提交不了。我们不光得写 Commit message 而且还应该写的清晰明了，说明本次提交的目的。
```bash
$ git commit -m "提交信息"
```
在编辑器中写commit message
```bash
$ git commit
```
写好 Commit message 好处多多：

1、统一团队Git commit 日志风格

2、方便日后 Reviewing Code

3、帮助我们写好 Changelog 

4、能很好的提升项目整体质量

## **Commit 提交规范**

业界比较推崇 Angular 的 commit 规范  http://suo.im/4rsYee

Commit message 包括三个部分：Header，Body 和 Footer。完整格式如下：

```html
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

**1) type**

提交 commit 的类型，包括以下几种

\- feat: 新功能

\- fix: 修复问题

\- docs: 修改文档

\- style: 修改代码格式，不影响代码逻辑

\- refactor: 重构代码，理论上不影响现有功能

\- perf: 提升性能

\- test: 增加修改测试用例

\- chore: 修改工具相关（包括但不限于文档、代码生成等）

**2) scope**

修改文件的范围，比如：视图层、控制层、docs、config, plugin

**3) subject**

\- subject 是 commit 目的的简短描述（用一句话清楚的描述这次提交做了什么），不超过50个字符

**4) body**

\- 补充 subject 添加详细说明，可以分成多行，适当增加原因、目的等相关因素，也可不写

5 ) footer

\- 当有非兼容修改(Breaking Change)时必须在这里描述清楚

\- 关闭issue或是链接到相关文档，如 Closes #1, Closes #2, #3

## 使用 commitzen

commitzen 这个工具可以帮助我们写出规范的 Commit message。

GitHub：https://github.com/commitizen/cz-cli

**![img](https://user-gold-cdn.xitu.io/2018/5/8/1633eab52fa3de92?w=557&h=300&f=jpeg&s=37427)**

使用npm 全局安装

```bash
$ npm install -g commitizen
```

在项目中使用 angular 的 commit 规范

```bash
$ commitizen init cz-conventional-changelog --save-dev --save-exact
```

然后我们就可以愉快的使用 git cz 代替 git commit 命令了。当然我们也可也将其加到npm script 中

```javascript
"script": {
    "commit": "git cz"
}
```

然后直接使用npm run commit

## 使用 gitmoji

gitmoji 和 commitzen的作用都是帮助我们写出规范的commit message，不过gitmoji有更好玩的 moji表情。（ 用moji来表示type ）

GitHub：https://github.com/carloscuesta/gitmoji-cli

安装使用
```bash
# 安装
$ npm i -g gitmoji-cli
# 使用
$ gitmoji -c
```

挑选个符合场景的moji 提交本次更改

![img](https://user-gold-cdn.xitu.io/2018/5/8/1633eab52fbb6fdc?w=1548&h=918&f=gif&s=1926466)

## 使用Git hooks

与其他版本控制系统一样，当某些重要事件发生时，Git 可以调用自定义脚本，Git 有很多钩子可以用来调用脚本自定义 Git。在 .git -> hooks 目录下可以看到示例。 例如：pre-commit就是在代码提交之前做些事情。如果你打开了 hooks 目录里面的 `*.sample` 文件，你可以看见里面写的shell脚本。但是我想用 Js 写 hooks 咋办？husky、pre-commit就能满足你。

现在我们想实现一个提交代码时使用 Eslint 进行代码检查的功能

**先来看pre-commit**

GitHub：https://github.com/observing/pre-commit

```
# 下载安装
npm install --save-dev pre-commit
```

在package.json 中配置pre-commit

```
"scripts": {    
   "lint": "eslint [options] [file|dir|glob]*",
},
"pre-commit": [    
   "lint",
]
```

现在提交代码试试

```
git commit -m 'Keep calm and commit'
```

**再试试 husky**

GitHub：https://github.com/typicode/husky

开始还是下载，不过这儿我们用的是 @next 版，使用方法与正式版略有不同。

```
npm install husky@next --save-dev
```

和 pre-commit 一样，还是在package.json中配置。但是处理pre-commit钩子它还可以做的更多。

```json
// package.json
{
  "scripts": {
    "lint": "eslint [options] [file|dir|glob]*",
  },
  "husky": {
    "hooks": {
      "pre-commit": "npm lint",
      "pre-push": "..."
    }
  }
}
```

本文介绍了如何规范的编写Commit message，以及使用commentzen与gitmoji这两个工具来帮助我们写出规范的Commit message。最后介绍了下Git hooks，并通过 husky 或是 pre-commit 与 Eslint结合使用来构建一个代码检测工作流。当然，你还可以做的更多。