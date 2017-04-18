# 简介

- 概述
- JM 约定
- JM 包含的开源项目

## 概述

JM 是基于 JavaScript 语言实现的一组开源项目的集合。它的目标，是使得 JM 可以用来快速开发和部署应用程序。

## JM 约定

所有子项目都被定义在命名空间 jm 内，从而防止定义冲突。

```javascript
//例如
jm.Class
jm.Object
jm.ajax
```

首字母大写为类，小写为函数、对象或者变量，类名首字母小写为实例化该类的函数。

```javascript
//jm.Object为类
var obj = new jm.Object();

//等同于
var obj = jm.object();

//jm.Object 和 jm.object 的原始定义如下
jm.Object = jm.Class.extend({
    _className: 'object',

    attr: function (attrs) {
        for (var key in attrs) {
            if(key === 'className'){
                continue;
            }

            this[key] = attrs[key];
        }
    }
});

jm.object = function(){
    return new jm.Object();
};
```

## JM 包含的开源项目

核心库 Core [jm-core] (https://github.com/jm-root/jm-core)

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
