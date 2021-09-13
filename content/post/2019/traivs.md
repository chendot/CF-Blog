---
date: 2019-12-06
title: Traivs
sidebar: false
description: GitHub貌似没有那么龟速了，对比一下它采用的traivs和gitlab-ci
categories:
  - "技术文档"
tags: ["SCM","DevOps"]
---

Anyway, Travis is one of the favorite bands I love. I like the song Walking in the sun.

![travis](/img/travis-0016.jpg)

## Travis CI 的钩子与生命周期

### Travis的钩子

Travis 有不同的阶段,他提供了7个钩子。

- before_install：install 阶段之前执行
- before_script：script 阶段之前执行
- after_failure：script 阶段失败时执行
- after_success：script 阶段成功时执行
- before_deploy：deploy 步骤之前执行
- after_deploy：deploy 步骤之后执行
- after_script：script 阶段之后执行

### 生命周期

- before_install
- install
- before_script
- script
- aftersuccess or afterfailure
- [OPTIONAL] before_deploy
- [OPTIONAL] deploy
- [OPTIONAL] after_deploy
- after_script
