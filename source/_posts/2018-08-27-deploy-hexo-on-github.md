---
title: 原创 | 更快更好的使用 Hexo 写个人博客
date: 2018-08-25 20:37:39
categories: 技术
tags:
  - Hexo
  - Github Page
  - Travis CI
---

> 预计阅读时间为：8 分钟

## 前言

欢迎访问 [Caifx 的个人博客](https://caifx.github.io)。本文将介绍如何通过 Hexo，Github Page 和 Travis CI 来提升你的写作体验，让你更快更好的使用 Hexo，专注于写作过程

<!-- more -->

- [Hexo](https://hexo.io/zh-cn/)：快速、简洁且高效的博客框架
- [Github Page](https://pages.github.com/)：用来部署你的博客网站，相当于服务器
- [Travis CI](https://travis-ci.org/)：持续化构建工具，相当于有个机器人帮你完成一些固定的操作

## 本文环境配置

```
node -v	// v8.11.4
hexo -v // hexo-cli: 1.1.0

// 操作系统：Debian GNU/Linux 9.5 (stretch)
```

### Github 配置

#### 首先创建个人博客仓库

**1. 登录 [Github](https://github.com/)**

**2. 点击 "+" 号, 选择 "New Repository(新建仓库)"**

**3. 仓库名格式必须是: username.github.io**

![PqBb5j.png](https://s1.ax1x.com/2018/08/27/PqBb5j.png)

#### 接着生成 Personal access tokens

**1. 点击 Settings**

![PqWMo6.png](https://s1.ax1x.com/2018/08/27/PqWMo6.png)

**2. Developer settings > Personal access tokens > Generate new token**

除了 delete_repo 没有勾选, 其他都勾选了. 最后一定要记下生成的秘钥, 下次就看不见了

![PqWKdx.png](https://s1.ax1x.com/2018/08/27/PqWKdx.png)

### Hexo 配置

```bash
// 全局安装 Hexo CLI
npm install hexo-cli -g	


// 初始化 hexo 项目并命名为 blog
hexo init blog					


// 克隆仓库到本地
git clone git@github.com:caifx/caifx.github.io.git


// 新建 source 分支
cd caifx.github.io
git checkout -b source


// 把 blog 文件夹内容都复制到 caifx.github.io 文件夹下
cd ..
cp -a blog/. caifx.github.io/


// 使用 Next 主题
cd caifx.github.io/
git clone https://github.com/theme-next/hexo-theme-next themes/next


// 删除 Next 主题的 .git 文件夹
cd themes/next
rm -r .git/


// 编辑 caifx.github.io/_config.yml
找到 theme: landscape 更改为 theme: next


// 本地测试 hexo
hexo server
```

### Travis CI 配置

**1. 登录 [Travis](https://travis-ci.org/)**

**2. 点击 Add New Repository**

**3. 打开 caifx.github.io 仓库的开关并点击 Settings**

![PqWZQJ.png](https://s1.ax1x.com/2018/08/27/PqWZQJ.png)

**4. 配置 GH_TOKEN**

![Pqf96H.png](https://s1.ax1x.com/2018/08/27/Pqf96H.png)

**5. 配置 caifx.github.io/.travis.yml**

没有这个文件,就新建一个

`user.name`, `user.email`, `GH_REF` 部分要修改成自己的信息

```yaml
# 指定语言环境
language: node_js

# 指定需要sudo权限
sudo: required

# 指定node_js版本
node_js: stable

# 指定缓存模块，可加快编译速度。
cache:
  directories:
    - node_modules

# 指定博客源码分支
branches:
  only:
    - source

before_install:
  - npm install -g hexo-cli

install:
  - npm install

before_script:
  - git config user.name "caifx"
  - git config user.email "123456789@qq.com"
  

# 执行清除缓存，生成网页操作
script:
  - hexo clean
  - hexo generate

after_success:
- cd ./public
- git init
- git add .
- git commit -m "Travis CI Auto Builder"
- git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master

env:
 global:
   - GH_REF: github.com/caifx/caifx.github.io.git

```

### 发布

最后，将 source 分支推送到 caifx.github.io 仓库上，Travis CI 就会根据 `.travis.yml` 的配置自动执行脚本。过几分钟后，前往  ` https://caifx.github.io/`，即可查看到博客内容已经更新了

### 更多...

- Hexo 站点的配置和 [Next 主题](https://theme-next.org/) 的配置
- 学习 Git 的有关操作

