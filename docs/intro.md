# 简介

## 概述

JM 微服务框架是一组开源项目的集合。它的目标，是用来快速开发和部署基于微服务架构的应用解决方案，主要包含核心库、中间件库、应用模板和应用。

### 核心库

JM 微服务框架核心库包括基础库 core, 微服务库 ms 和微服务器库 server。

1. 基础库 core 包含一组基础支持库，主要包括：
    - jm-module 提供模块化支持, 用于实现插件式功能扩展。
    
    - jm-event 提供一个通用的轻量级的事件机制。
    
    - jm-logger 提供日志服务。
    
    - jm-err 定义了常用的错误。
    
1. 微服务库 ms 依赖基础库 core。

    提供一种新的路由定义方式，定义一次可以支持多种通讯协议，例如 Http，Websocket 甚至 UDP 等等，这带来的好处是部署时更加灵活，例如对于最终用户提供 Http 协议，而对于微服务之间的通讯采用更加高效的 Websocket 协议或者 UDP 协议。

1. 微服务器库 server 依赖基础库 core 和微服务库 ms。

    帮助开发者把精力集中在应用层面的服务 service、控制器 controller 及路由 router 的开发，而不必关注底层的实现。特别的，由于 jm-server 采用了模块化设计，开发者可以把多个微服务应用集中在一个 jm-server 中作为单体应用部署，这样可以兼容传统的软件开发模式，更加灵活。

### 中间件库

用于扩展微服务库 ms 的功能, 例如数据库支持等。

### 应用模板

基于核心库提供了一个微服务器应用模板 server-template, 帮助开发者快速创建一个微服务应用。

### 应用

框架自身也提供了常用的微服务应用，无需开发，开箱即用，帮助开发者快速部署一套基于微服务架构的解决方案。这些应用包括网关服务 gateway, 配置服务 config, 单点登陆服务 sso, 鉴权服务 acl, 通行证服务 passport, 用户服务 user, 消息服务 mq 等。  

## 典型微服务架构方案

网关服务 gateway 负责转发请求到对应的微服务，配置服务config完成统一配置，通行证服务 passport 负责用户注册登陆，单点登陆服务 sso 负责令牌 token 的创建和管理，鉴权服务 acl 负责权限控制。

所有服务都基于微服务器库 server 实现。

![](../images/plan.svg)

## 框架包含的开源项目

### 核心库

1. [基础库 core](https://github.com/jm-root/core)

1. [微服务库 ms](https://github.com/jm-root/ms)

1. [微服务器库 server](https://github.com/jm-root/server)

### 应用模板

1. [微服务器应用模板 server template](https://github.com/jm-root/server-template)

### 应用

1. [网关服务 gateway](https://github.com/jm-root/gateway)

1. [配置服务 config](https://github.com/jm-root/jm-config)

1. [单点登陆服务 sso](https://github.com/jm-root/jm-sso)

1. [鉴权服务 acl](https://github.com/jm-root/acl)

1. [通行证服务 passport](https://github.com/jm-root/passport)

1. [用户服务 user](https://github.com/jm-root/user)

1. [消息服务 mq](https://github.com/jm-root/mq)
