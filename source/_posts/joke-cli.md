---
title: Node命令行工具开发【看段子】
date: 2017-03-18
---

# Node命令行工具开发【看段子】
> 你有没有上班想看笑话却又怕领导发现的经历？现在我们就用几十行代码写一个命令行看笑话段子的小程序，从此无需担心领导的视察。这篇文章和上一篇差不多都是命令行小工具开发，不过本篇更偏向于小爬虫的开发

## 总览：命令行看段子小程序
我们先来看看我们今天的小目标：
- 先为它起个命吧：`joke-cli`
- 爬取并提取 [糗事百科的笑话](http://www.qiushibaike.com/)
- 输出到命令行*按下回车显示一条段子*

## 初识[新手村]

下面我们将介绍今天用到的主要模块

### cheerio

> **`cheerio`**可理解为服务器端的jQuery，基本用法与jQuery一样。有了它，我们在写小爬虫时就可抛开那可爱又可恨的正则表达式了。从此拥抱幸福生活。

用法如下：

    ```javascript
    let cheerio = require('cheerio')
    
    // 将html文本转化成可用jQuery操作的dom,,然后你就可以把它当成jQuery了
    let $ = cheerio.load('<h2 class="title">Hello world</h2>')
     
    $('h2.title').text('Hello there!')
    $('h2').addClass('welcome')
     
    $.html()
    //=> <h2 class="title welcome">Hello there!</h2> 
    ```

*更多请参考[cheerio](https://cheerio.js.org/)*

### superagent

`superagent`专注于处理服务端/客户端的http请求，用法如下：

    ```javascript
     request
       .get(url)
       .end(function(err, res){
    
       });
    ```

就是这么简答，你已经学会使用它了，别懵逼，这三行代码，已经完全够我们本次示例的使用了。*额，当然了，更多的请移步官方文档*
- [superagent](http://visionmedia.github.io/superagent/)
- [[译] SuperAgent中文使用文档](https://cnodejs.org/topic/5378720ed6e2d16149fa16bd)

### 初出茅庐【先拿百度练练手】

我们已经介绍了今天的两大主角，那就先来练练手，就用百度吧

    ```javascript
    const superAgent = require('superagent')
    const cheerio = require('cheerio')
    const URL = 'http://www.baidu.com/'
    
    // 发起GET请求
    superAgent
      .get(URL) 
      .end((err, res)=>{
      	if(err) console.error(err)
        // 用cheerio处理返回的html
      	const $ = cheerio.load(res.text)
        // 找到并打印出按钮#su的值
        console.log($('#su').val())  // 百度一下
      })   
    ```

ok,现在已经了解并能使用这两个模块，更多的探索在自己，我们应当再用写时间去阅读其文档，对其有深入的了解。接下来就是用刚学的这些知识为你涨姿势了。

## 开始开发`joke-cli`

### 初始化项目

    ```bash
    $ mkdir joke-cli
    $ cd joke-cli
    $ npm init
    $ npm install cheerio superagent colors --save //colors 输出美化
    ```

新建好bin/index.js文件，并加入package.json文件中

    ```json
    "bin": {
        "joke-cli": "./bin/index.js"
     }
    ```

现在执行`npm link`。我们的小项目就初始化成功了，就可以认真思考代码了

### 首先分析糗事百科url

我们打开糗事百科会发现它的URL还是很简单，由于我们只是爬取段子所以url如下`http://www.qiushibaike.com/text/page/2/4965899`，2就是页数。

![糗事百科](http://ommpd2lnj.bkt.clouddn.com/qiushibaike-url.png)

### 开始编写index.js

    ```
    #!/usr/bin/env node
    
    const superAgent = require('superagent')
    const cheerio = require('cheerio')
    
    let url = 'http://www.qiushibaike.com/text/page/'
    let page = 1
    
    superAgent
    	.get(url+page) 
        .end((err, res)=>{
          	if(err) console.error(err)
            console.log(res.text)
        })
    ```

`f12`查看糗事百科的HTML结构，可以发先每条笑话都在一个`div.article`中，笑话的内容则在`div.content`中

![糗事百科HTML](http://ommpd2lnj.bkt.clouddn.com/qiushibaike-html.png)

在分析完html结够后，现在可以用我们用cheerio很容易就可以取出笑话

    ```javascript
    ···
    .end((err, res)=>{
      if(err) console.error(err)
      const $ = cheerio.load(res.text)
      const jokeList = $('.article .content span')
      jokeList.each(function(i, item){
        console.log($(this).text()) //将打印出每条笑话
      })    
    })	
    ···
    ```

### 实现命令行交互

这里我们需要用到readlinem模块

#### Readline(逐行读取) 

> `require('readline')` 模块提供了一个接口，用于从[可读流](http://nodejs.cn/api/stream.html)（如 [`process.stdin`](http://nodejs.cn/api/process.html#process_process_stdin)）读取数据，每次读取一行。 基本用法如下：

 *使用 `readline.Interface` 类实现一个简单的命令行界面：*

    ```javascript
    const readline = require('readline');
    const rl = readline.createInterface({
      input: process.stdin,
      output: process.stdout,
      prompt: '请输入> '
    });
    
    //rl.prompt() 方法会在 output 流中新的一行写入 readline.Interface 实例配置后的 prompt，用于为用户提供一个可供输入的新的位置
    rl.prompt();
    
    rl.on('line', (line) => {
      switch(line.trim()) {
        case 'hello':
          console.log('world!');
          break;
        default:
          console.log(`你输入的是：'${line.trim()}'`);
          break;
      }
      rl.prompt();
    }).on('close', () => {
      console.log('再见!');
      process.exit(0);
    });
    ```

*更多参考[Node.js中文网](http://nodejs.cn/api/readline.html)*

### 改写index.js实现命令行交互功能

    ```javascript
    #!/usr/bin/env node
    
    const superAgent = require('superagent')
    const cheerio = require('cheerio')
    const readline = require('readline')
    const colors = require('colors')
    // 创建readlinde.Interface 实现命令行交互
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout,
        prompt: ' ?  您正在使用joke-cli,按下回车查看笑话 ? >>>'
    })
    let url = 'http://www.qiushibaike.com/text/page/'
    let page = 1
    
    // 使用数组来存放笑话
    let jokeStories = []
    // 载入笑话并存入数组中
    function loadJokes(){
      	// 数组中的笑话不足三条时就请求下一页的数据
        if(jokeStories.length<3){
            superAgent
            .get(url+page) 
            .end((err, res)=>{
                if(err) console.error(err)
                const $ = cheerio.load(res.text)
                const jokeList = $('.article .content span')
                jokeList.each(function(i, item){
                    jokeStories.push($(this).text()) //存入数组
                })
                page++            
            })
        }
    }
    
    rl.prompt()
    loadJokes()
    // line事件 每当 input 流接收到接收行结束符（\n、\r 或 \r\n）时触发 'line' 事件。 通常发生在用户按下 <Enter> 键或 <Return> 键。
    // 按下回车键显示一条笑话
    rl.on('line', (line) => {
        if(jokeStories.length>0){
            console.log('======================')
            console.log(jokeStories.shift().bgCyan.black) //用colors模块改变输出颜色
            loadJokes()
        }else{
            console.log('正在加载中~~~'.green)
        }
        rl.prompt()
    }).on('close', () => {
        console.log('Bye!')
        process.exit(0)
    })
    ```

这里我们用了一个数组存放笑话，每按下回车，就显示一条(`shift()`删除并返回数组第一个元素)，当数组中不足三条时就请求新的一页

## 总结

到此，我们的joke-cli就开发完成。此时我们应该了解了superagent, cheerio， readline等模块的使用。这会儿应该趁热打铁，快去好好看看这些模块吧

## 相关链接
- [cheerio](https://cheerio.js.org/)
- [superagent](http://visionmedia.github.io/superagent/)
- [译)SuperAgent中文使用文档](https://cnodejs.org/topic/5378720ed6e2d16149fa16bd)
- [Node.js中文网](http://nodejs.cn/api/readline.html)
- [colors.js](https://github.com/marak/colors.js/)




