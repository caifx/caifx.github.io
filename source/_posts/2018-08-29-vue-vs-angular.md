---
title: 原创 | 与 Angular 的差异中学习 Vue
date: 2018-08-29 09:57:04
updated:
categories: 技术
tags:
  - Vue
  - Angular
---

> 预计阅读时间: x 分钟

## 前言

在通过官网学习 Vue 的过程中, 因为我(博客: `https://caifx.github.io`)对 Angular 更熟悉一些, 所以本文侧重于比较 Vue 和 Angular 的异同, 并且不会重新讲解 Vue 的细节, 如有需要请移步[官网](https://cn.vuejs.org)

<!-- more -->

## 搭建一个最简单的 Vue 环境

新建一个文件夹, 再新建2个文件, 分别命名为 `hello.html` 和 `hello.js` , 代码如下:

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Hello Vue</title>   
</head>

<body>
  <!-- Vue 容器开始 -->
  <div id="app">
    {{message}}
  </div>
  <!-- Vue 容器结束 -->

  
  <!-- 必须在 Vue 容器声明后面引入 -->
  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
  <script src="./hello.js"></script>
</body>

</html>
```

```javascript
var app = new Vue({
  el: '#app',	// 通过 CSS 选择器语法指向 Vue 容器
  data: {			// data 属性储存变量
    message: 'Hello Vue!!!'
  }
})
```

通过上面的代码, 我们可以有个简单的认识: Vue 就是在 HTML 中声明一个容器(`id="app"`), 在 JavaScript 中通过 **Vue 函数** 创建出一个 Vue 实例, 然后向 Vue 实例传递一个**选项对象**来配置好相关内容, 如通过 el 属性指向容器(`el: "#app"`), 从而实现模板和实例的绑定. 在 data 属性中声明变量, methods 属性中声明函数..., 最后就可以通过 Vue 语法在模板中使用了

而在 Angular 中, 则通过 `@Component` 装饰器的 `templateUrl` 来实现模板和实例的绑定, 从而实现对**整个**模板的管理. 通过类属性声明变量, 类方法声明函数(在构建由 Vue.js 管理所有模板的[单页面应用程序 (SPA - single page application)](https://en.wikipedia.org/wiki/Single-page_application) 时, 则跟 Angular 类似).  Angular 的示例如下:

```html
<div>{{message}}</div>
```

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  message: 'Hello Vue!!!'

  constructor() {}

}

```

## 核心特性的比较


|            | Angular                    | Vue                                   |
| ---------- | -------------------------- | ------------------------------------- |
| 插值表达式 | ｛｛　插值表达式　｝｝     |  ｛｛　插值表达式 ｝｝                       |
| 属性绑定   | [属性名]="变量"            | v-bind:属性名="变量" / :属性名="变量" |
| 事件绑定   | (事件名)="方法"            | v-on:事件名="方法" / @事件名="方法"   |
| 判断       | *ngIf="表达式"             | v-if="表达式"                         |
| 循环       | *ngFor="let item of items" | v-for="item in items"                 |
| 双向绑定   | [(ngModel)]="变量"         | v-model="变量"                        |

## Vue 实例

```javascript
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!!!'
  },
  methods: {
    reverseMessage: function() {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```

- 每一个 Vue 实例都是通过 `Vue()` 函数, 再传入一个选项对象来创建的

- 要获取选项对象的属性(也就是实例属性和实例方法), 通过添加前缀 `$` 来和自定义的属性区分开

  ```javascript
  app.$el === document.getElementById('app') // => true
  
  // $watch 是一个实例方法
  app.$watch('a', function (newValue, oldValue) {
    // 这个回调将在 `app.a` 改变后调用
  })
  ```

- 生命周期钩子(**与 Angular 不是一一对应的关系**)


  | Angular               | Vue           |
  | --------------------- | ------------- |
  | ngOnChanges           | beforeCreate  |
  | ngOnInit              | created       |
  | ngDoCheck             | beforeMount   |
  | ngAfterContentInit    | mounted       |
  | ngAfterContentChecked | beforeUpdate  |
  | ngAfterViewInit       | updated       |
  | ngAfterViewChecked    | beforeDestroy |
  | ngOnDestroy           | destroyed     |