---
title: 微服务
date: 2020-05-20
sidebar: false
description: 系统的改进好似生物的进化，功能愈加复杂，职责越分越细。目的都是为了更好的适应变化的环境。
categories:
  - "随笔"
  - IT
---

一年来除了例行机械地忙碌于常规的、繁琐的日常事务性工作外，欣慰的是做了些许DevOps的改进。接下来得再玩点新花式，对现有管理的几个系统架构上做些许改进。逐步调整为微服务架构。

### 优点
- 服务独立，耦合性低
- 单个服务依赖少，启动快速
- 更加适合敏捷开发，针对单个服务发布版本快速
- 职责更加明确，服务拆分利于团队之间分工
- 服务可以动态按需扩容
- 代码复用，每个服务提供REST API，所有基础服务必须抽离

### 劣势
- 调用复杂性高，各模块通过Http来通信，这当中会产生诸如网络、容错、调用等多种问题
- 独立的数据库，分布式事务
- 测试难度增加，涉及大量接口，自动化测试尤为重要
- 运维难度提升，部署、监控更为复杂

和生物的渐进式演化一样，系统重构最好是采用循序渐进的模式。做好重构规划，抽出业务服务，再抽出这个产品所依赖的基础服务。尽量将重要的，影响重大的模块放到后面。

不要想着一步登天，在保障现有业务稳定运行情况下，稳步调整改进。

## Spring Cloud 主要模块
- Eureka：服务注册中心，用于管理服务
- Ribbon：基于客户端的负载均衡组件
- Hystrix：容错框架，防止服务雪崩效应
- Feign：Web服务客户端，简化Http接口调用
- Zuul：API网关，控制路由转发、请求过滤
- Config：分布式配置管理
- Sleuth：服务跟踪
- Stream：构建消息驱动的微服务应用框架
- Bus：消息总线