# 简介

- 概述
- JM 约定
- JM 典型微服务架构方案
- JM 包含的开源项目

## 概述

JM 是一组开源项目的集合。它的目标，是用来快速开发和部署基于微服务架构的应用程序。

## JM 约定

首字母大写为类，小写为函数、对象或者变量，类名首字母小写为实例化该类的函数。

## JM 典型微服务架构方案

gateway负责转发请求到对应的微服务，config服务完成统一配置，passport负责用户注册登陆，sso负责单点登陆，acl负责鉴权。

所有服务都基于jm-server实现。

jm-server是一个通用服务器框架，帮助开发者把精力集中在应用层面的服务及路由的开发，而不必关注底层的实现。特别的，由于jm-server采用了模块化设计，开发者可以灵活的把多个微服务集中在一个jm-server中部署，这样可以兼容传统的软件开发模式，更加灵活。

jm-ms作为JM微服务架构的核心模块，提供一种新的路由定义方式，定义一次可以支持多种通讯协议，例如Http，Websocket甚至UDP等等，这带来的好处是部署时更加灵活，例如对于最终用户提供Http协议，而对于微服务之间的通讯采用更加高效的Websocket协议或者UDP协议。

module提供模块化支持。

event提供一个通用的轻量级的事件机制。

logger提供日志服务。

err定义了常用的错误。

![](../images/plan.svg)

## JM 包含的开源项目

核心库 Core [core] (https://github.com/jm-root/core)

模块 Module [jm-module] (https://github.com/jm-root/jm-module)

Log4js日志 Log4js [jm-log4js] (https://github.com/jm-root/jm-log4js)

微服务 MS [jm-ms] (https://github.com/jm-root/ms)

通用服务器 Server [jm-server] (https://github.com/jm-root/server)

通用开发包 SDK [sdk] (https://github.com/jm-root/sdk)

路由服务 Gateway [gateway] (https://github.com/jm-root/gateway)

配置服务 Config [jm-config] (https://github.com/jm-root/jm-config)

鉴权服务 ACL [acl] (https://github.com/jm-root/acl)

单点登陆服务 SSO [jm-sso] (https://github.com/jm-root/jm-sso)

用户服务 User [user] (https://github.com/jm-root/user)

通行证服务 Passport [passport] (https://github.com/jm-root/passport)

消息服务 MQ [mq] (https://github.com/jm-root/mq)

数据库访问库 db [db] (https://github.com/jm-root/db)
