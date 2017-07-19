# 简介

- 概述
- JM 约定
- JM 典型微服务架构方案
- JM 包含的开源项目

## 概述

JM 是一组开源项目的集合。它的目标，是用来快速开发和部署基于微服务架构的应用程序。

## JM 约定

首字母大写为类，小写为函数、对象或者变量，类名首字母小写为实例化该类的函数。

为了支持浏览器中使用，定义了公共命名空间jm（相当于定义了global.jm），从而防止定义冲突。

```javascript
//例如
jm.EventEmitter
jm.Err
jm.utils
jm.ajax
```

node中可以直接使用公共命名空间，但是不推荐。

```javascript
var event = require('jm-event');

//推荐
var e = new event.EventEmitter();

//可以用，但不推荐
var e = new jm.EventEmitter();

```

ES6中的用法：

```javascript
import event from 'jm-event';

//推荐
var e = new event.EventEmitter();

//可以用，但不推荐
var e = new jm.EventEmitter();

```

## JM 典型微服务架构方案

Gateway负责转发请求到对应的微服务，Config服务完成统一配置，Passport负责用户注册登陆，SSO负责单点登陆，ACL负责鉴权。

所有服务都基于jm-server实现。

jm-server是一个通用服务器框架，这样开发者可以把精力集中在对于服务及路由的定义和实现，而不必关注底层的实现。特别的，由于jm-server采用了模块化设计，开发者可以灵活的把多个微服务集中在一个jm-server中部署，这样可以兼容传统的软件开发模式，更加灵活。

jm-ms作为JM微服务架构的核心模块，提供一种新的路由定义方式，定义一次可以支持多种通讯协议，例如Http，Websocket甚至UDP等等，这带来的好处是部署时更加灵活，例如对于最终用户提供Http协议，而对于微服务之间的通讯采用更加高效的Websocket协议或者UDP协议。

module提供模块化支持。

event提供一个通用的轻量级的事件机制。

logger提供日志服务。

err定义了常用的错误。

![](../images/plan.svg)

## JM 包含的开源项目

模块 Module [jm-module] (https://github.com/jm-root/jm-module)

事件 Event [jm-event] (https://github.com/jm-root/jm-event)

错误 Err [jm-err] (https://github.com/jm-root/jm-err)

日志 Logger [jm-logger] (https://github.com/jm-root/jm-logger)

Log4js日志 Log4js [jm-log4js] (https://github.com/jm-root/jm-log4js)

AJAX库 Ajax [jm-ajax] (https://github.com/jm-root/jm-ajax)

微服务 MS [jm-ms] (https://github.com/jm-root/jm-ms)

消息队列 MQ [jm-mq] (https://github.com/jm-root/jm-mq)

数据库访问库 Dao [jm-dao] (https://github.com/jm-root/jm-dao)

实体组件系统 ECS [jm-ecs] (https://github.com/jm-root/jm-ecs)

设备 Device [jm-device] (https://github.com/jm-root/jm-device)

通用服务器 Server [jm-server] (https://github.com/jm-root/jm-server)

通用客户端 Client [jm-client] (https://github.com/jm-root/jm-client)

通用开发包 SDK [jm-sdk] (https://github.com/jm-root/jm-sdk)

配置服务器 Config [jm-config] (https://github.com/jm-root/jm-config)

权限控制 ACL [jm-acl] (https://github.com/jm-root/jm-acl)

单点登陆 SSO [jm-sso] (https://github.com/jm-root/jm-sso)

路由服务器 Gateway [jm-gateway] (https://github.com/jm-root/jm-gateway)

通用用户模块 User [jm-user] (https://github.com/jm-root/jm-user)

统一管理后台 OMS [jm-oms] (https://github.com/jm-root/jm-oms)

Gate服务器 Gate [jm-gate] (https://github.com/jm-root/jm-gate)

IP数据库 IP [jm-ip] (https://github.com/jm-root/jm-ip)

AOP库 Aop [jm-aop] (https://github.com/jm-root/jm-aop)

类 Class [jm-class] (https://github.com/jm-root/jm-class)
