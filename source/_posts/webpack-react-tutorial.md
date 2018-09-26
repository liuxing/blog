---
title: 上手webpack，搭建react开发环境 
date: 2018-07-18
---

![webpack](https://i.loli.net/2018/09/26/5bab3bd5bdc74.png)

随着互联网的蓬勃发展，web 应用越来越复杂，一个前端web项目有着一大堆依赖包和复杂的JavaScript代码。然而在 web端，模块化的支持来的很缓慢，CSS很容易发生冲突，JavaScript语法较为松散……存在着种种急需解决的问题，为了简化开发的复杂度，蓬勃发展的前端社区涌现出了很多好的实践方法及工具：各种模块化规范、CSS预处理、CSS后处理器、TypeScript、Grunt / Gulp等构件工具以及webpack、browserify、rollup、parcel等模块打包工具等等。

在前端构建中，代码模块打包几乎就是最重要的一部分，而webpack是模块打包工具中最流行最具代表性的一个。webpack 是一个模块打包器。它的主要目标是将 JavaScript 文件打包在一起，打包后的文件用于在浏览器中使用，但它也能够胜任转换、打包或包裹任何资源。

## 上手 webpack

本文将通过实例讲解 webpack，最后完成一个 react 开发环境集成babel、eslint、sass。

新建一个 `webpack-react ` 初始化 npm 并安装 webpack

```bash
mkdir webpack-react && cd webpack-react
npm init -y
npm install webpack webpack-cli --save-dev
```

进入`webpack-react` 新建三个文件 `index.html`  `index.js`  `hello.js`

```diff
  webpack-react
  |- package.json
+ |- dist
+   |- index.html
+ |- /src
+   |- index.js
+   |- hello.js
```

**src/hello.js**

```
// hello.js
export default function () {
  const element= document.createElement('div')
  element.innerHTML = '欢迎关注公众号JavaScript之禅'
  return element
}
```

**src/index.js**

```javascript
// index.js
import hello from "./hello.js"
document.body.appendChild(hello())
```

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Getting Started</title>
</head>
<body>
  <script src="./main.js"></script>
</body>
</html>
```
在命令行执行 `npx webpack`  试试，运行该命令会将资源打包到 `dist` 目录下的 `main.js`。 webpack 4.x 可以零配置构建。此时你会看见一个警告：未设置mode，webpack 4.x 提供了mode配置来使用相应的内置优化，有生产模式（production）、开发模式（development）和不设置（none）三种。但是为了更好的使用我们往往需要自己写配置文件。

先来看看 webpack 的常用配置项， 详细参考 https://webpack.docschina.org/configuration/

```javascript
module.exports = {
    mode: 'production',      // 模式
    entry: '',               // 入口文件
    output: {},              // 出口文件
    module: {},              // 处理对应模块
    plugins: [],             // 对应的插件
}
```

按照项目，我们从0写个最简单的配置 `webpack.config.js` 它的实现的功能就像零配置一样。

```javascript
// webpack.config.js
const path = require('path')

module.exports = {
    entry: './src/index.js',        // 入口文件
    output: {
        filename: 'main.js',        // 打包后的文件名称
        path: path.resolve('dist')  // 打包后的目录，必须是绝对路径
    }
}
```

## 启动devServer

现在我们想要看到效果都需要，运行命令打包后再在浏览器中查看，现在我们使用 `webpack-dev-server` 来免去这些繁琐的步骤。`webpack-dev-server` 为我们提供了一个简单的 web 服务器，并且能够实时重新加载(live reloading)

```bash
$ npm install --save-dev webpack-dev-server
```

修改配置文件，告诉开发服务器(dev server)，在哪里查找文件、在哪个端口启动：

```javascript
// webpack.config.js
const path = require('path')

module.exports = {
    entry: './src/index.js',        // 入口文件
    output: {
        filename: 'main.js',        // 打包后的文件名称
        path: path.resolve('dist')  // 打包后的目录，必须是绝对路径
    },
    devServer: {
        contentBase: './dist',
        open: true,
        port: 3000
    }
}
```

执行 `npx webpack-dev-server` 就可以将这个服务起起来，我们将它加到 `npm script` 中去

```javascript
...
"scripts": {
    "dev": "webpack-dev-server",
    "build": "webpack"
},
...
```

开发时直接运行`npm run dev` 即可，打包则运行`npm run build`

## 使用 source map

当 webpack 打包源代码时，可能会很难追踪到错误和警告在源代码中的原始位置，为了更容易地追踪错误和警告，JavaScript 提供了 source map功能，将编译后的代码映射回原始源代码。当然如果你设置了mode为development，他是默认开启的。

```javascript
module.exports = {
    ...
	devtool: 'inline-source-map'
    ...
}
```

## 配置Html模板

现在项目的 `index.html` 是手动创建的，如果更改打包后的文件的名称就又要去手动更改一次。我们使用 **html-webpack-plugin** 插件来搞定，生成一个自动引用你打包后的JS文件的新 `index.html`

```bash
$ npm install --save-dev html-webpack-plugin
```

修改配置文件

```javascript
const HtmlWebpackPlugin  = require('html-webpack-plugin')

module.exports = {
    ...
    plugins: [
      new HtmlWebpackPlugin()
    ]
}
```

## 使用sass

`Loaders` 是 `webpack` 提供的最激动人心的功能之一了。通过使用不同的`loader`实现对不同格式的文件的处理。如sass转css，jsx转js。

这一步我们先来配置CSS，为了从 JavaScript 模块中 `import` 一个 CSS 文件，你需要在 `module` 配置中安装并添加 style-loader和 css-loader。这儿我还用了sass，所以多下载了`sass-loader` 与  `node-sass`

```bash
$ npm install  --save-dev css-loader style-loader sass-loader node-sass
```

**webpack.config.js**

```javascript
// 使用sass
...
module: {
    rules: [
        {
            test: /\.scss$/,
            use: [
                'style-loader',
                'css-loader'
                'sass-loader'
            ]
        }
    ]
}
...

// ============
// 如果你不需要sass 配置css即可
// ============
...
module: {
    rules: [
        {
            test: /\.css$/,
            use: [
                'style-loader',
                'css-loader'
            ]
        }
    ]
}
...
```

新建一个`hello.scss`， 在 `hello.js` 中引用

**hello.scss**

```css
.hello {
  color: red;
}
```

**hello.js**

```javascript
// hello.js
import './hello.scss'

export default function () {
    const element= document.createElement('div')
    element.innerHTML = '欢迎关注公众号JavaScript之禅'
    element.classList.add('hello')
    return element
}
```

执行`npm run build` 在浏览器中打开 `index.html`就能看见样式生效了

## 使用autoprefixer 添加CSS3前缀

由于CSS3很多属性还需要添加各个浏览器的前缀，使用postcss的autoprefixer可以帮助我们方便的处理这个问题

```bash
$ npm i -D postcss-loader autoprefixer
```

新建一个  `postcss.config.js` 文件配置下postcss

```javascript
module.exports = {
  plugins: [
      require('autoprefixer')
  ]
}
```

在webpack配置中添加postcss-loader

```javascript
module: {
    rules: [
      {
        test: /\.js$/,
        include: /src/,
        exclude: /node_modules/,
        use: [
          'babel-loader'
        ]
      },
      {
        test: /\.scss$/,
        use: [
          'style-loader',
          'css-loader',
          'postcss-loader', // 添加 postcss-loader
          'sass-loader'
        ]
      }
    ]
  },
```

## 分离CSS

在多数情况下打包时都会进行CSS 分离，以便在生产环境中节省加载时间。在4.x以前的版本中，我们使用 extract-text-webpack-plugin 来拆分CSS。在4.x版本中webpack推荐使用 mini-css-extract-plugin 替代。

```bash
$ npm install --save-dev mini-css-extract-plugin
```

在配置文件中配置下这个插件

```javascript
...
{
    test: /\.scss$/,
    use: [
        // 'style-loader',
        MiniCssExtractPlugin.loader,
        'css-loader',
        'postcss-loader',
        'sass-loader'
    ]
}
...
plugins: [
    ...
    new MiniCssExtractPlugin({
      filename: "static/css/[name].css",
      chunkFilename: "static/css/[id].css"
    })
  ]
```

运行`npm run build`，webpack会将CSS单独打包出来。

如果重复执行`npm run build` `dist`目录下会有上次打包后的文件，这儿使用 clean-webpack-plugin 这个插件来清理

```bash
$ npm i -D clean-webpack-plugin
```

在配置文件中配置我们的需要清理的文件夹 

```javascript
...
plugins: [
    ...
    new CleanWebpackPlugin(['dist'])
]
...
```

## 使用 babel 编译 react 

前面说了，我们的目标是搭建react开发环境，现在就配置 babel-loader 来转码 react。

```bash
$ npm install --save-dev babel-loader babel-core babel-preset-env babel-preset-react
$ npm install --save react react-dom
```
新增一个`.babelrc`文件配置babel

```json
{
  "presets": [
    "env", 
    "react"
  ]
}

```

修改webpack.config.js，增加一个处理react的loader

```javascript
module: {
    rules: [
      ...
      {
        test: /\.js$/,
        include: /src/,
        exclude: /node_modules/,
        use: [
          'babel-loader'
        ]
      },
      ...
   ]
  },
```

删除 `src` 目录下的所有文件，新建一个`index.js`、`index.scss`

```scss
// index.scss
body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}
```

```jsx
// index.js
import React from 'react'
import ReactDOM from 'react-dom'
import './index.scss'

ReactDOM.render(
  <h1>欢迎关注公众号JavaScript之禅</h1>
  ,document.getElementById('root'))

```

我们需要修改HtmlWebpackPlugin的配置，在`public`文件夹中新建`index.html` 用来作为生成html文件的模板

```html
<!DOCTYPE html>
<html lang="zh-cn">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <link rel="manifest" href="/manifest.json">
    <link rel="shortcut icon" href="/favicon.ico">
    <title>React App</title>
  </head>
  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>
    <div id="root"></div>
  </body>
</html>
```

修改webpack.config.js中的配置

```javascript
...
plugins: [
    new HtmlWebpackPlugin({
        template: path.resolve(__dirname, '../public/index.html'),
        hash: true
    })
]
...
```

现在就可以愉快的编写react了。

## 处理图片字体等资源

前面说过webpack处理各种文件就是配置各种loader，对于图片、字体等资源我们可以使用file-loader来处理

```bash
$ npm install file-loader --save-dev
```

修改webpack的配置文件，让其支持图片文字等资源

```javascript
...
{
  test: /\.(png|svg|jpg|gif)$/,
  use: [
    {
      loader: 'file-loader',
      options: {
        name: 'static/images/[name].[hash:8].[ext]'
      }
    }
  ]
},
{
  test: /\.(woff|woff2|eot|ttf|otf)$/,
  use: [
    'file-loader'
  ]
}
...
```

## 使用 ESLint 检查代码

ESLint是一个javascript代码检测工具，它可以用于检查常见的JavaScript代码错误，也可以进行代码风格检查，这样我们就可以根据自己的喜好指定一套ESLint配置，然后应用到所编写的项目上，从而实现辅助编码规范的执行，有效控制项目代码的质量。

在webpack中我们可以使用eslint-loader来检查代码，笔者我比较喜欢 **JavaScript  Standard Style** ，现在就来配置下

```bash
$ npm install --save-dev eslint eslint-loader eslint-config-standard eslint-plugin-standard eslint-plugin-promise eslint-plugin-import eslint-plugin-node  eslint-plugin-react
```

新建 `.eslintrc` 配置eslint规则

```javascript
{
  "extends": [
    "standard",
    "plugin:react/recommended"
  ]
}
```

在webpack配置中新增eslint-loader

```javascript
...
module: {
    rules: [
      {
        enforce: 'pre',
        test: /\.js$/,
        include: /src/,
        exclude: /node_modules/,
        loader: 'eslint-loader'
      }
      ...
    ]
    ...
}
...
```

## 启用HMR

模块热替换(HMR - Hot Module Replacement)功能会在应用程序运行过程中替换、添加或删除模块，而无需重新加载整个页面。我们是讲快速上手搭建react开发环境的，在此就不细说HMR了。我们直接使用 react-hot-loader 这个模块。

```bash
$ npm --save-dev install react-hot-loader
```

在`.babelrc`中添加配置

```javascript
{
  ...
  "plugins": ["react-hot-loader/babel"]
}
```

在`src/App.js`中使用react-hot-loader

```javascript
import React from 'react'
import { hot } from 'react-hot-loader'
 
class App extends Component {}
 
export default hot(module)(App)
```

除此之外还需要在webpack.config.js中添加如下配置，并且修改下devServer的配置

```javascript
plugins: [
    ...
	new webpack.NamedModulesPlugin(),
    new webpack.HotModuleReplacementPlugin()
],
devServer: {
    contentBase: './dist',
    port: 3000,
    open: true,
    hot: true
}
```

现在运行`npm run dev` 修改项目代码试试。如果你跟着教程一步一步走到这儿，你会发现修改CSS并不会生效，这是因为，我们用了MiniCssExtractPlugin来拆分CSS文件，在开发环境中我们还是使用style-loader即可，同时开发环境还应该启用 sourceMap 方便调试。

下一节再讲开发环境与生产环境的区分，并在此基础上做些调整优化。