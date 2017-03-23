# 核心库 Core
[jm-core] (https://github.com/jm-root/jm-core)

- 根 root
- 错误定义 ERR
- 日志 logger
- 工具 utils
- 类 Class
    - 类的定义
    - 类的继承
    - 类的保留属性
- 对象 Object
- 事件 EventEmitter
- 标签对象 TagObject
- 随机数 Random

## 根 root

***注意，开发人员一般不需要使用 jm.root 。***

jm.root 类似于 global，用于存放公共变量。

jm.root.registries 为 jm 的注册表。

## 错误定义 ERR

jm.ERR 统一定义了常用的错误，格式如下，其中 err 表示错误的编码，msg 表示错误的信息。

```javascript
jm.ERR = {
    SUCCESS: {
        err: 0,
        msg: 'Success'
    },
    .....
};
```

| 错误      | 编码      | 信息  |
| ----- |:-------------:| :-----|
|SUCCESS|0|Success|
|FAIL|1|Fail|
|FA_SYS|2|System Error|
|FA_NETWORK|3|Network Error|
|FA_PARAMS|4|Parameter Error|
|FA_BUSY|5|Busy|
|FA_TIMEOUT|6|Time Out|
|FA_ABORT|7|Abort|
|FA_NOTREADY|8|Not Ready|
|OK|200|OK|
|FA_BADREQUEST|400|Bad Request|
|FA_NOAUTH|401|Unauthorized|
|FA_NOPERMISSION|403|Forbidden|
|FA_NOTFOUND|404|Not Found|
|FA_INTERNALERROR|500|Internal Server Error|
|FA_UNAVAILABLE|503|Service Unavailable|

## 日志 logger

```javascript
//默认日志
var logger = jm.logger;
['trace','debug','info','warn','error','fatal'].forEach(function(level) {
    logger[level]('logger test: %s %s', level, Date.now());
});

//分类日志
var logger = jm.getLogger('main');
['trace','debug','info','warn','error','fatal'].forEach(function(level) {
    logger[level]('logger test: %s %s', level, Date.now());
});
```

## 工具 utils

jm.utils.formatJSON 格式化 json 对象为字符串

```javascript
var obj = {
    name: 'test',
    value: 123
};

jm.utils.formatJSON(obj);
```

## 类 Class
### 类的定义
```javascript
var Object = jm.Class.extend({
    //类的名称
    _className: 'object',

    //构造函数
    ctor: function (opts) {
        this._name = 'test';
    },

    //类的属性定义
    properties: {
        name: { get: 'getName', set: 'setName' }
    },

    getName: function() {
        return this._name;
    },

    setName: function(name) {
        this._name = name;
    },

    //类的方法定义
    method1: function(opts, cb) {
        cb(null, true);
    }
});

//test
var obj = new Object();
console.log(obj.name);
```

### 类的继承

```javascript
var Object = jm.Class.extend({
    //类的名称
    _className: 'object',

    //构造函数
    ctor: function (opts) {
        console.log('Object ctor called');
        this._name = 'test';
    },

    //类的方法定义
    method1: function(opts, cb) {
        console.log('Object.method1 called');
        cb(null, true);
    }
});

var ObjectB = Object.extend({
    //类的名称
    _className: 'objectB',

    //构造函数
    ctor: function (opts) {
        //调用父级构造函数
        this._super(opts);
        this._name = 'testB';
        console.log('ObjectB ctor called');
    },

    //类的方法定义
    method1: function(opts, cb) {
        //调用父级函数
        this._super(opts, cb);
        console.log('ObjectB.method1 called');
    }
});

//test
var obj = new ObjectB();
obj.method1(null, function(err, doc){
    console.log(doc);
});
```

### 类的保留属性

className 被定义为只读属性，表示类的名称，在类定义时通过 _className 赋值，如果没有赋值，则继承父类的值。

```javascript
var Object = jm.Class.extend({
    _className: 'object',
});
var ObjectB = Object.extend({
});
console.log(new Object().className);
console.log(new ObjectB().className);
//输出 object
```

## 对象 Object
## 事件 EventEmitter
## 标签对象 TagObject
## 随机数 Random
