---
title: 《Node.js从入门到上线》入门篇 （持续更新中）
date: 2018-06-08
---

最近利用空闲时间写了一个从入门到上线的的node实战教程《Node.js从入门到上线》A blog build with Koa2. 目前还在更新中，入门篇已基本成型。

本项目使用es6语法，采用Koa2 + mongoose 搭建了一个博客系统，实现了文章管理、用户登录注册、权限控制、分类管理等功能。

GitHub: [https://github.com/liuxing/node-blog](https://github.com/liuxing/node-blog) 欢迎star 

## 目录

[1.1 Node.js 的安装与配置](https://github.com/liuxing/abc-blog/tree/master/docs/1.1Node.js%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.md)

- [安装Node.js](https://github.com/liuxing/abc-blog/tree/master/docs/1.1Node.js%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.md#%E5%AE%89%E8%A3%85nodejs)
- [使用nvm](https://github.com/liuxing/abc-blog/tree/master/docs/1.1Node.js%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.md#%E4%BD%BF%E7%94%A8-nvm)
- [一些有用的工具](https://github.com/liuxing/abc-blog/tree/master/docs/1.1Node.js%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.md#%E4%B8%80%E4%BA%9B%E6%9C%89%E7%94%A8%E7%9A%84%E5%B7%A5%E5%85%B7)
- [hello-node](https://github.com/liuxing/abc-blog/tree/master/docs/1.1Node.js%E7%9A%84%E5%AE%89%E8%A3%85%E4%B8%8E%E9%85%8D%E7%BD%AE.md#hello-node)

[1.2 Node.js 基础概览](https://github.com/liuxing/abc-blog/tree/master/docs/1.2Node.js%E5%9F%BA%E7%A1%80%E6%A6%82%E8%A7%88.md)

- [node模块](https://github.com/liuxing/abc-blog/tree/master/docs/1.2Node.js%E5%9F%BA%E7%A1%80%E6%A6%82%E8%A7%88.md#node%E6%A8%A1%E5%9D%97)
- [npm包管理器](https://github.com/liuxing/abc-blog/tree/master/docs/1.2Node.js%E5%9F%BA%E7%A1%80%E6%A6%82%E8%A7%88.md#npm%E6%A8%A1%E5%9D%97%E7%AE%A1%E7%90%86%E5%99%A8)

[2.1 Koa2初体验](https://github.com/liuxing/abc-blog/tree/master/docs/2.1Koa2%E5%88%9D%E4%BD%93%E9%AA%8C.md)

- [Hello Koa2](https://github.com/liuxing/abc-blog/tree/master/docs/2.1Koa2%E5%88%9D%E4%BD%93%E9%AA%8C.md#hello-koa2)
- [使用supervisor 或者 nodemon](https://github.com/liuxing/abc-blog/tree/master/docs/2.1Koa2%E5%88%9D%E4%BD%93%E9%AA%8C.md#%E4%BD%BF%E7%94%A8supervisor-%E6%88%96%E8%80%85-nodemon)

[2.2 MongoDB的安装及使用](https://github.com/liuxing/abc-blog/tree/master/docs/2.2MongoDB%E5%AE%89%E8%A3%85%E5%8F%8A%E4%BD%BF%E7%94%A8.md)

[3.1 开发前的项目配置](https://github.com/liuxing/abc-blog/tree/master/docs/3.1%E5%BC%80%E5%8F%91%E5%89%8D%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%85%8D%E7%BD%AE.md)

- [规划项目目录结构](https://github.com/liuxing/abc-blog/tree/master/docs/3.1%E5%BC%80%E5%8F%91%E5%89%8D%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%85%8D%E7%BD%AE.md#%E8%A7%84%E5%88%92%E9%A1%B9%E7%9B%AE%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)
- [使用editorconfig](https://github.com/liuxing/abc-blog/tree/master/docs/3.1%E5%BC%80%E5%8F%91%E5%89%8D%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%85%8D%E7%BD%AE.md#%E4%BD%BF%E7%94%A8editorconfig)
- [使用commitizen](https://github.com/liuxing/abc-blog/tree/master/docs/3.1%E5%BC%80%E5%8F%91%E5%89%8D%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%85%8D%E7%BD%AE.md#%E4%BD%BF%E7%94%A8commitizen)
- [使用eslint](https://github.com/liuxing/abc-blog/tree/master/docs/3.1%E5%BC%80%E5%8F%91%E5%89%8D%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%85%8D%E7%BD%AE.md#%E4%BD%BF%E7%94%A8eslint)
- [使用Git hooks自动检查代码](https://github.com/liuxing/abc-blog/tree/master/docs/3.1%E5%BC%80%E5%8F%91%E5%89%8D%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%85%8D%E7%BD%AE.md#%E4%BD%BF%E7%94%A8git-hooks%E8%87%AA%E5%8A%A8%E6%A3%80%E6%9F%A5%E4%BB%A3%E7%A0%81)

[3.2 把项目跑起来](https://github.com/liuxing/abc-blog/tree/master/docs/3.2%E6%8A%8A%E9%A1%B9%E7%9B%AE%E8%B7%91%E8%B5%B7%E6%9D%A5.md)

- [router](https://github.com/liuxing/abc-blog/tree/master/docs/3.2%E6%8A%8A%E9%A1%B9%E7%9B%AE%E8%B7%91%E8%B5%B7%E6%9D%A5.md#router)
- [配置模板引擎](https://github.com/liuxing/abc-blog/tree/master/docs/3.2%E6%8A%8A%E9%A1%B9%E7%9B%AE%E8%B7%91%E8%B5%B7%E6%9D%A5.md#%E9%85%8D%E7%BD%AE%E6%A8%A1%E6%9D%BF%E5%BC%95%E6%93%8E)
- [配置静态资源](https://github.com/liuxing/abc-blog/tree/master/docs/3.2%E6%8A%8A%E9%A1%B9%E7%9B%AE%E8%B7%91%E8%B5%B7%E6%9D%A5.md#%E9%85%8D%E7%BD%AE%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90)

[3.3 使用mongoose操作数据库](https://github.com/liuxing/abc-blog/tree/master/docs/3.3%E6%93%8D%E4%BD%9C%E6%95%B0%E6%8D%AE%E5%BA%93.md)

- [设计Schema](https://github.com/liuxing/abc-blog/tree/master/docs/3.3%E6%93%8D%E4%BD%9C%E6%95%B0%E6%8D%AE%E5%BA%93.md#%E8%AE%BE%E8%AE%A1schema)
- [使用model](https://github.com/liuxing/abc-blog/tree/master/docs/3.3%E6%93%8D%E4%BD%9C%E6%95%B0%E6%8D%AE%E5%BA%93.md#%E4%BD%BF%E7%94%A8model)

[3.4用户注册与登录](https://github.com/liuxing/abc-blog/blob/master/docs/3.4%E7%94%A8%E6%88%B7%E6%B3%A8%E5%86%8C%E4%B8%8E%E7%99%BB%E5%BD%95.md)

- [cookie与session](https://github.com/liuxing/abc-blog/blob/master/docs/3.4%E7%94%A8%E6%88%B7%E6%B3%A8%E5%86%8C%E4%B8%8E%E7%99%BB%E5%BD%95.md#cookie%E4%B8%8Esession)
- [用户注册](https://github.com/liuxing/abc-blog/blob/master/docs/3.4%E7%94%A8%E6%88%B7%E6%B3%A8%E5%86%8C%E4%B8%8E%E7%99%BB%E5%BD%95.md#%E7%94%A8%E6%88%B7%E6%B3%A8%E5%86%8C)
- [用户登录](https://github.com/liuxing/abc-blog/blob/master/docs/3.4%E7%94%A8%E6%88%B7%E6%B3%A8%E5%86%8C%E4%B8%8E%E7%99%BB%E5%BD%95.md#%E7%94%A8%E6%88%B7%E7%99%BB%E5%BD%95)
- [用户登出](https://github.com/liuxing/abc-blog/blob/master/docs/3.4%E7%94%A8%E6%88%B7%E6%B3%A8%E5%86%8C%E4%B8%8E%E7%99%BB%E5%BD%95.md#%E7%94%A8%E6%88%B7%E7%99%BB%E5%87%BA)

[3.5 koa2中间件开发](https://github.com/liuxing/abc-blog/blob/master/docs/3.5koa2%E4%B8%AD%E9%97%B4%E4%BB%B6%E5%BC%80%E5%8F%91.md)

- [koa2 中间件机制](https://github.com/liuxing/abc-blog/blob/master/docs/3.5koa2%E4%B8%AD%E9%97%B4%E4%BB%B6%E5%BC%80%E5%8F%91.md#koa2-%E4%B8%AD%E9%97%B4%E4%BB%B6%E6%9C%BA%E5%88%B6)
- [消息闪现中间件](https://github.com/liuxing/abc-blog/blob/master/docs/3.5koa2%E4%B8%AD%E9%97%B4%E4%BB%B6%E5%BC%80%E5%8F%91.md#%E6%B6%88%E6%81%AF%E9%97%AA%E7%8E%B0%E4%B8%AD%E9%97%B4%E4%BB%B6)

[3.6 文章增删改查](https://github.com/liuxing/abc-blog/blob/master/docs/3.6%E6%96%87%E7%AB%A0%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5.md)

- [文章模型设计](https://github.com/liuxing/abc-blog/blob/master/docs/3.6%E6%96%87%E7%AB%A0%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5.md#%E6%96%87%E7%AB%A0%E6%A8%A1%E5%9E%8B%E8%AE%BE%E8%AE%A1)
- [文章发表](https://github.com/liuxing/abc-blog/blob/master/docs/3.6%E6%96%87%E7%AB%A0%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5.md#%E6%96%87%E7%AB%A0%E5%8F%91%E8%A1%A8)
- [文章列表与详情](https://github.com/liuxing/abc-blog/blob/master/docs/3.6%E6%96%87%E7%AB%A0%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5.md#%E6%96%87%E7%AB%A0%E5%88%97%E8%A1%A8%E4%B8%8E%E8%AF%A6%E6%83%85)
- [文章编辑与删除](https://github.com/liuxing/abc-blog/blob/master/docs/3.6%E6%96%87%E7%AB%A0%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5.md#%E6%96%87%E7%AB%A0%E7%BC%96%E8%BE%91%E4%B8%8E%E5%88%A0%E9%99%A4)

[3.7 用户权限控制](https://github.com/liuxing/abc-blog/blob/master/docs/3.7%E7%94%A8%E6%88%B7%E6%9D%83%E9%99%90%E6%8E%A7%E5%88%B6.md)

- [登录状态检查](https://github.com/liuxing/abc-blog/blob/master/docs/3.7%E7%94%A8%E6%88%B7%E6%9D%83%E9%99%90%E6%8E%A7%E5%88%B6.md#%E7%99%BB%E5%BD%95%E7%8A%B6%E6%80%81%E6%A3%80%E6%9F%A5)
- [管理权限控制](https://github.com/liuxing/abc-blog/blob/master/docs/3.7%E7%94%A8%E6%88%B7%E6%9D%83%E9%99%90%E6%8E%A7%E5%88%B6.md#%E7%AE%A1%E7%90%86%E6%9D%83%E9%99%90%E6%8E%A7%E5%88%B6)

[3.8 评论功能](https://github.com/liuxing/abc-blog/blob/master/docs/3.8%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD.md)

- [设计评论的模型](https://github.com/liuxing/abc-blog/blob/master/docs/3.8%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD.md#%E8%AE%BE%E8%AE%A1%E8%AF%84%E8%AE%BA%E7%9A%84%E6%A8%A1%E5%9E%8B)
- [发布留言](https://github.com/liuxing/abc-blog/blob/master/docs/3.8%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD.md#%E5%8F%91%E5%B8%83%E7%95%99%E8%A8%80)
- [显示留言](https://github.com/liuxing/abc-blog/blob/master/docs/3.8%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD.md#%E5%8F%91%E5%B8%83%E7%95%99%E8%A8%80)
- [删除留言](https://github.com/liuxing/abc-blog/blob/master/docs/3.8%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD.md#%E5%88%A0%E9%99%A4%E7%95%99%E8%A8%80)

[3.9 一些安全问题](https://github.com/liuxing/abc-blog/blob/master/docs/3.9%E4%B8%80%E4%BA%9B%E5%AE%89%E5%85%A8%E9%97%AE%E9%A2%98.md)

- [XSS的防范](https://github.com/liuxing/abc-blog/blob/master/docs/3.9%E4%B8%80%E4%BA%9B%E5%AE%89%E5%85%A8%E9%97%AE%E9%A2%98.md#xss%E7%9A%84%E9%98%B2%E8%8C%83)
- [CSRF的防范](https://github.com/liuxing/abc-blog/blob/master/docs/3.9%E4%B8%80%E4%BA%9B%E5%AE%89%E5%85%A8%E9%97%AE%E9%A2%98.md#csrf-%E7%9A%84%E9%98%B2%E8%8C%83)

[3.10 分类管理](https://github.com/liuxing/abc-blog/blob/master/docs/3.10%E6%96%87%E7%AB%A0%E5%88%86%E7%B1%BB.md)

- [分类模型](https://github.com/liuxing/abc-blog/blob/master/docs/3.10%E6%96%87%E7%AB%A0%E5%88%86%E7%B1%BB.md#%E5%88%86%E7%B1%BB%E6%A8%A1%E5%9E%8B%E8%AE%BE%E8%AE%A1)
- [分类管理主页](https://github.com/liuxing/abc-blog/blob/master/docs/3.10%E6%96%87%E7%AB%A0%E5%88%86%E7%B1%BB.md#%E5%88%86%E7%B1%BB%E7%AE%A1%E7%90%86%E4%B8%BB%E9%A1%B5)
- [新增与删除](https://github.com/liuxing/abc-blog/blob/master/docs/3.10%E6%96%87%E7%AB%A0%E5%88%86%E7%B1%BB.md#%E6%96%B0%E5%A2%9E%E5%88%86%E7%B1%BB)

[3.11 分页功能](https://github.com/liuxing/abc-blog/blob/master/docs/3.11%E5%88%86%E9%A1%B5%E5%8A%9F%E8%83%BD.md)

- [MongoDB分页原理](https://github.com/liuxing/abc-blog/blob/master/docs/3.11%E5%88%86%E9%A1%B5%E5%8A%9F%E8%83%BD.md#mongodb-%E5%AE%9E%E7%8E%B0%E5%88%86%E9%A1%B5%E5%8E%9F%E7%90%86)
- [实现一个基本的分页器](https://github.com/liuxing/abc-blog/blob/master/docs/3.11%E5%88%86%E9%A1%B5%E5%8A%9F%E8%83%BD.md#%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%9F%BA%E6%9C%AC%E7%9A%84%E5%88%86%E9%A1%B5%E5%99%A8)
- [高级一点儿的分页器](https://github.com/liuxing/abc-blog/blob/master/docs/3.11%E5%88%86%E9%A1%B5%E5%8A%9F%E8%83%BD.md#%E9%AB%98%E7%BA%A7%E4%B8%80%E7%82%B9%E5%84%BF%E7%9A%84%E5%88%86%E9%A1%B5%E5%99%A8)

[3.12 koa2错误处理及404](https://github.com/liuxing/abc-blog/blob/master/docs/3.12koa2%E9%94%99%E8%AF%AF%E5%A4%84%E7%90%86%E5%8F%8A404.md)

[3.13 单元测试 更新中]

...

持续更新中，未来将逐步发布【上线篇】：域名服务器选购、服务器配置、Nginx等等。实现线上部署