---
title: JSON 入门教程
date: 2017-04-05
---

> JSON的全称是”JavaScript Object Notation”，意思是JavaScript对象表示法，它是一种基于文本，独立于语言的轻量级数据交换格式，类似 XML但比 XML 更小、更快，更易解析

### 初识

JSON是Web开发领域最知名的技术权威Douglas Crockford创造

- JSON 指的是 JavaScript 对象表示法（JavaScript Object Notation）
- JSON 是轻量级的文本数据交换格式
- JSON 独立于语言 
- JSON 具有自我描述性，更易理解

JSON建构于两种结构：

- “名称/值”对的集合（A collection of name/value pairs）。不同的语言中，它被理解为*对象（object）*，纪录（record），结构（struct），字典（dictionary），哈希表（hash table），有键列表（keyed list），或者关联数组 （associative array）。
- 值的有序列表（An ordered list of values）。在大部分语言中，它被理解为数组（array）。

这些都是常见的数据结构。事实上大部分现代计算机语言都以某种形式支持它们。这使得一种数据格式在同样基于这些结构的编程语言之间交换成为可能。

### JSON语法
#### 两种表示结构

JSON有两种表示结构，对象和数组。

- 对象是一个无序的“‘名称/值’对”集合。一个对象以`{`（左括号）开始，`}`（右括号）结束。每个“名称”后跟一个`:`（冒号）；“‘名称/值’ 对”之间使用`,`（逗号）分隔。

  ```json
  {
      "name": "xing",
      "age": 999
  }
  ```

  ​

- 数组是值（value）的有序集合。一个数组以`[`（左中括号）开始，`]`（右中括号）结束。值之间使用`,`（逗号）分隔。

  ```json
  [
      {
          key1:value1,
          key2:value2 
      },
      {
           key3:value3,
           key4:value4   
      }
  ]
  ```


#### 语法规则

- 数据在名称/值对中
- 数据由逗号分隔
- 大括号保存对象
- 中括号保存数组

#### JSON 值可以是：

- 数字（整数或浮点数）
- 字符串（在双引号中）
- 逻辑值（true 或 false）
- 数组（在中括号中）
- 对象（在大括号中）
- null

### 在JavaScript中使用JSON

> JSON 通常用于与服务端交换数据。在接收服务器数据时一般是字符串。我们可以使用 JSON.parse() 方法将数据转换为 JavaScript 对象，使用 JSON.stringify() 方法将 JavaScript 对象转换为字符串.

- ```javascript
  JSON.parse(text[, reviver])
  ```

- ````javascript
  JSON.stringify(value[, replacer[, space]])
  ````

- eval()方法 *存在性能和安全问题不建议使用*


首先我们定义一个对象,由于JSON使用用JavaScript编写的，所以对JSON的操作无异于JavaScript对数组与对象的操作

```javascript
let Obj = {  
  name: "xing", 
  age: "99", 
  hobby: ["吃", "喝", "玩"]
}
```

服务器一般返回JSON字符串，我们用 `JSON.stringify() `将这个对象转换成JSON字符串模拟服务器返回的数据，然后再用`JSON.parse()`解析成JSON对象来使用

```javascript
let jsonStr = JSON.stringify(Obj) // string: {"name":"xing","age":"99","hobby":["吃","喝","玩"]}
let jsonObj = JSON.parse(jsonStr) // Obect: { name: 'xing', age: '99', hobby: [ '吃', '喝', '玩' ] }
```

#### JSON增删改查

```javascript
// 读取
let myName = jsonObj.name
console.log(myName) // xing
// 新增
josnObj.sex = "male"
console.log(josnObj) //{ name: 'xing', age: '99', hobby: [ '吃', '喝', '玩' ], sex: 'female' }
// 修改
josnObj.sex = "female"
console.log(josnObj) // { name: 'xing', age: '99', hobby: [ '吃', '喝', '玩' ], sex: 'female' }
// 删除
delete josnObj.sex
console.log(josnObj) // { name: 'xing', age: '99', hobby: [ '吃', '喝', '玩' ] }
```

用`for in`遍历JSON数据

```javascript
for(let x in jsonObj){
  console.log(`${x}:${jsonObj[x]}`)
}
/*
name:xing
age:99
hobby:吃,喝,玩
*/
```

到此，我们了解JSON的使用，JSON已经是JavaScript标准的一部分。目前，主流的浏览器对JSON支持都非常完善。应用JSON，我们可以从XML的解析中摆脱出来，对那些应用AJAX的Web 2.0网站来说，JSON是目前最灵活的轻量级方案。

### 参考链接：

- [json.org](http://www.json.org/json-zh.html)
- [菜鸟教程](http://www.runoob.com/json/json-intro.html)
- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JSON在线解析](http://www.json.cn/)