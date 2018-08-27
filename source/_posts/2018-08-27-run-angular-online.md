---
title: 原创 | 在线演示你的 Angular 项目
date: 2018-08-27 21:15:34
updated: 2018-08-27 21:49:05
categories: 技术
tags:
  - Angular
  - Github
  - Stackblitz
---

> 预计阅读时间为：5 分钟

## 前言
辛辛苦苦创造出来的 Angular 项目，却无法向别人分享？买个云服务器又太费钱？放心，这里有妙招～

<!-- more -->

## 一、通过 Github Pages 展示

> 假设你能在本地运行一个 Angular 项目，并且能上传项目到 Github 上

1. 要求

   - Node.js 4.x
   - Git 1.7.6+
   - 通过 angular-cli 创建项目

2. 步骤

   1. 安装工具库

      `$ npm i -g angular-cli-ghpages`

   2. 在 Github 上新建项目并命名为 “run-angular-online”

   3. 编译 Angular 项目，并指定根地址

      `$ ng build --prod --base-href "/run-angular-online/"`

   4. 链接本地项目到远程仓库

      `$ git remote add origin git@github.com:caifx/run-angular-online.git`

   5. 发布到 Github

      `$ ngh` ，成功后提示 \*\*Successfully published!

3. 更多 `ngh` 使用方法，请[点击访问](https://github.com/angular-schule/angular-cli-ghpages)

## 二、通过 stackblitz 展示

> 继续使用第一步所使用的 Github 仓库为例子讲解 git@github.com:caifx/run-angular-online.git
>
> 这个方法非常简单，灵活和强大，请至 [官方文档](https://stackblitz.com/docs) 查看详情

1.  上传 master 分支（或者其他分支到仓库中）

    `$ git push -u origin master`

2.  访问 `https://stackblitz.com/github/用户名/仓库名/tree/分支名` 即可

    如 `https://stackblitz.com/github/caifx/run-angular-online/tree/master`
