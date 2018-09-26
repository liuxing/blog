---
title: VS Code上手与超实用插件安利
date:  2017-11-24
---

**工欲善其事必先利其器**

> Visual Studio Code (简称 VS Code / VSC) 是一款免费开源的现代化轻量级代码编辑器，支持几乎所有主流的开发语言的语法高亮、智能代码补全、自定义热键、括号匹配、代码片段、代码对比 Diff、GIT 等特性，支持插件扩展，并针对网页开发和云端应用开发做了优化。软件跨平台支持 Win、Mac 以及 Linux，运行流畅，可谓是微软的良心之作

**微软有 Visual Studio这个宇宙最强IDE，Visual Studio Code 自然也不会弱*(宇宙最强编辑器)***

说到代码编辑器，我们有必要提一提[Sublime Text](https://www.sublimetext.com/)还有[Atom](https://atom.io/)。在开始使用VS Code之前Sublime Text一直是我的主力编辑器，和[WebStorm](https://www.jetbrains.com/webstorm/) *（最强端前端开发工具）* 一起用。由于这篇文章主要介绍VS Code下面就简单概括下这几个：

Sublime Text：在我的日常使用中都挺满意，快速，稳定。唯一不爽是证书购买(虽然可以一直无限制使用)，没有开源

Atom：你们用着真不卡吗？还是我电脑配置太差，不过UI真的好看

VS code：微软开源，比sublime开源，比atom更快，比webstorm更轻，值得一提的是它用的壳是GitHub开源的Electron。

## 主要功能

Visual Studio Code首先是一个编辑器，它包含了高效的源代码编辑所需的功能*(最为一个编辑器，主要功能当然是代码编辑了)* 我们主要还是看看特色功能。

### 智能感知 Intellisense
智能感知是各种代码编辑功能的总称，包括代码完成，参数信息，快速信息和成员列表。智能感知功能也被称为“代码补全”，“内容帮助”和“代码提示”，这是一个现代编辑器最基本的自我修养了。

VS Code原生就支持JavaScript，TypeScript，JSON，HTML，CSS，Less和Sass的Intellisense，真正的强大之处在于，可以安装语言扩展来配置更丰富的IntelliSense*（几乎包括所有主流语言）*

![intellisense](https://code.visualstudio.com/assets/docs/editor/intellisense/intellisense.gif)

### 内置 Git

VS Code 内置了一个 Git GUI，支持最常用 Git 命令，这使得您可以很容易地看到您在项目中所做的更改。当然了，你可以通过扩展 让他更强大。

![scm](https://code.visualstudio.com/assets/docs/editor/versioncontrol/scm.png)

### 调试 Debugging

VS Code对[Node.js](https://nodejs.org/)运行时提供了内置的调试支持，并且可以调试JavaScript，TypeScript和任何其他被转换为JavaScript的语言。对于调试其他语言和运行环境时，我们也可以通过扩展来解决。

![debug](https://code.visualstudio.com/assets/docs/editor/debugging/debugging_hero.png)

### 终端命令行工具 Terminal

在VS Code中提供了一个功能齐全的集成终端，这非常方便，因为您不必切换窗口或更改现有终端的状态就可以快速执行命令

![integrated-terminal](https://code.visualstudio.com/assets/docs/editor/integrated-terminal/integrated-terminal.png)

### 扩展市场 Extensio

对于强大的插件市场来说，它自带的功能只是和开始而已。随着VS Code的流行，基本上你能找到所有你想要的插件*(实在找不到你还可以自己开发)*。

![extensions](https://code.visualstudio.com/assets/docs/editor/extension-gallery/extensions-popular.png)

更多请查阅[https://code.visualstudio.com/docs](https://code.visualstudio.com/docs)

## 开始上手

关于VS Code的使用也很简单

- 下载安装：去到它的官网[https://code.visualstudio.com/](https://code.visualstudio.com/)，下载对应版本，然后按照提示一直下一步就好
- 基本使用：在你安装好后，就可以看到有用的用户欢迎指引界面

![vscode](https://image-static.segmentfault.com/861/230/861230342-5a18fb69dc67d_articlex)

你可以在学习栏点击各项，迅速上手这个编辑器÷。下面主要就是推荐一些好用插件了，

### 插件安装方式

关于插件的安装，在看了`界面概述`后也应该是知道怎么安装了：

- 直接在扩展管理中键入你要下载的扩展名称或者关键字搜索下载
- 使用快捷键`⇧+⌘+P`，打开命令面板，输入如下命令即可

```javascript
ext install 扩展名
```

- 还可以从插件主页直接点击下载，他会唤起VS Code自动下载

## 基本配置

关于VS Code的各项设置，都在一个JSON文件中，左边是默认设置，右边是我们自己的设置，分为用户设置和工作区设置，我们只需要在右边我们编辑设置并保存即可。工作区设置后各项设置会保存在`.vscode`文件夹下。



![default-settings](https://az754404.vo.msecnd.net/public/default-settings.gif)

新安装一个编辑/IDE，最先干的就是调字体*(vscode 中可以直接按⌘加加号/减号调节字体)*，调颜色等外观配置了吧。

### 主题推荐

VS Code已经自带了很多个好看的主题，比如说我一直用的[Solarized Dark](http://ethanschoonover.com/solarized)

![themes](https://code.visualstudio.com/assets/docs/getstarted/themes/themes_hero.gif)

这里我再推荐几个不错的，

[**One Dark Pro**](https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme)：  Atom 标志性的主题

![One Dark Pro](https://raw.githubusercontent.com/Binaryify/OneDark-Pro/master/static/screenshot2.png)

[**Atom One Dark Theme**](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onedark)： 另一个基于 [One Dark](https://github.com/atom/one-dark-syntax) 的主题

![Atom One Dark Theme](https://raw.githubusercontent.com/akamud/vscode-theme-onedark/master/screenshots/preview.png)

[**Dracula Official**](https://marketplace.visualstudio.com/items?itemName=dracula-theme.theme-dracula)：超好看

![Dracula Official](https://draculatheme.com/assets/img/screenshots/vscode.png)

[**Material Theme**](https://marketplace.visualstudio.com/items?itemName=Equinusocio.vsc-material-theme) 一个简单而又干净的主题，有很多配置选项用于颜色配置
![Material Theme](https://i.imgur.com/JXb5aRO.jpg)

单单安装了主题还不够，我们还要好看的图标来足视觉体验：

[**vscode icons**](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons#overview)

![vscode icons](https://raw.githubusercontent.com/vscode-icons/vscode-icons/master/images/screenshot.gif)



[**Material Icon Theme**](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

![Material Icon Theme](https://raw.githubusercontent.com/PKief/vscode-material-icon-theme/master/images/fileIcons.png)

更多好看主题请浏览[https://marketplace.visualstudio.com/search?target=VSCode&category=Themes](https://marketplace.visualstudio.com/search?target=VSCode&category=Themes&sortBy=Downloads)



## 实用插件

[**filesize**](https://marketplace.visualstudio.com/items?itemName=mkxml.vscode-filesize)：在底部状态栏显示当前文件大小，点击后还可以看到详细创建、修改时间

[**Path Intellisense**](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)：文件路径补全，在你用任何方式引入文件系统中的路径时提供智能提示和自动完成

![Path Intellisense](http://i.giphy.com/iaHeUiDeTUZuo.gif)

[**vscode-fileheader**](https://marketplace.visualstudio.com/items?itemName=mikey.vscode-fileheader)：顶部注释模板，可定义作者、时间等信息，并会自动更新最后修改时间
![fileheader](https://raw.githubusercontent.com/zhaopengme/vscode-fileheader/master/fileheader.gif)

[**Git Lens**](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)：查看详细的git记录,内置功能很多
![Git Lens ](https://raw.githubusercontent.com/eamodio/vscode-gitlens/master/images/gitlens-preview.gif)

[**Git History (git log)**](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)：一个好用的Git 历史查看工具
![**Git History**](https://raw.githubusercontent.com/DonJayamanne/gitHistoryVSCode/master/images/gitLogv2.gif)
[**npm**](https://marketplace.visualstudio.com/items?itemName=eg2.vscode-npm-script): 可以直接在vscode执行npm的一些命令

![**npm**](https://raw.githubusercontent.com/Microsoft/vscode-npm-scripts/master/images/cmds.png)

[**Npm Intellisense**](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)：NPM 依赖补全，在你引入任何 node_modules 里面的依赖包时提供智能提示和自动完成

![**Npm Intellisense**](https://raw.githubusercontent.com/ChristianKohler/NpmIntellisense/master/images/auto_complete.gif)

[**Debugger for Chrome**](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)：让 vscode 映射 chrome 的 debug功能，静态页面都可以用 vscode 来打断点调试
![**Debugger for Chrome**](https://code.visualstudio.com/assets/docs/nodejs/extensions/chrome_debugger.png)

[**JavaScript (ES6) code snippets**](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)：常用的类声明、ES 模块声明、CMD 模块导入等

[**ESLint**](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)：代码语法检查

[**Beautify**](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)：格式化代码的工具

[**open-in-browser**](https://marketplace.visualstudio.com/items?itemName=coderfee.open-html-in-browser)： 在浏览器中预览HTM文件

[**HTML Snippets**](https://marketplace.visualstudio.com/items?itemName=abusaidm.html-snippets)：各种 HTML 标签片段

[**IntelliSense for CSS class names**](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion)：CSS 类名补全，会自动扫描整个项目里面的 CSS 类名并在你输入类名时做智能提示

[**Document This**](https://marketplace.visualstudio.com/items?itemName=joelday.docthis)： js 的注释模板![Document This](https://raw.githubusercontent.com/joelday/vscode-docthis/master/images/demo.gif)

[**Settings Sync**](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)：同步你得设置和插件

## 结语
我们从外观配置开始到插件推荐结束，到此基本上你就能打造出一个有自己风格强大编辑器，开发效率自然也是很高。你有什么好用的插件？欢迎留言交流！让更多的人知道。

同时，建议移步官网看看[https://code.visualstudio.com/](https://code.visualstudio.com/)，那儿有更全更细的文档，有助于我们更好的使用它。
