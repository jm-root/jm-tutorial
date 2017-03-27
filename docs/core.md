# 核心库 Core
[jm-core] (https://github.com/jm-root/jm-core)

- 引入
- 模块 module
    - 模块化设计
    - 模块的定义
    - 模块的加载、使用和卸载
- 错误定义 ERR
- 日志 logger
- 工具 utils
- 类 Class
    - 类的定义
    - 类的继承
    - 类的保留属性
- 对象 Object
- 事件 EventEmitter
    - EventEmitter 简介
    - EventEmitter#on(name, fn, caller)
    - EventEmitter#once(name, fn, caller)
    - EventEmitter#removeListener(name, fn, caller)
    - EventEmitter#removeAllListeners(name)
    - EventEmitter#listeners(name)
    - EventEmitter#emit(name, arg1, arg2, arg3, arg4, arg5)
- 标签对象 TagObject
- 随机数 Random

## 引入
install：

```javascript
npm install --save jm-core
```

ES6：

```javascript
import _ from 'jm-core';
let jm = _();
jm.logger.debug('works.');

```

node：

```javascript
var jm = require('jm-core')();
jm.logger.debug('works.');

//也可以采用全局变量jm，不推荐
require('jm-core');
jm.logger.debug('works.');

```

browser：

```
<script src="dist/js/jm-core.js"></script>
```

## 模块 module
### 模块化设计

为了方便扩展， jm 采用了模块化设计理念，一切都是模块。

模块可以动态加载和卸载。

### 模块的定义

ES6：

```javascript
// module1.js
export default ($, name = 'module1') => {
    $[name] = {
        toString: () => {
            return 'this is a module';
        }
    };
    return {
        name: name,
        unuse: ($) => {
            delete $[name];
        }
    };
};
```

node：

```javascript
// module1.js
module.exports = function ($, name) {
    name || (name = 'module1');
    $[name] = {
        toString: function () {
            return 'this is a module';
        }
    };
    return {
        name: name,
        unuse: function (_) {
            delete $[name];
        }
    };
};
```

### 模块的加载、使用和卸载

ES6：

```javascript
import $ from 'jm-core';
import module1 from './module1';

//加载
let jm = $()
        .use(module1)
    ;

// 使用加载的模块
jm.logger.debug(jm.module1.toString());

//卸载
jm.unuse ('module1');

```

node：

```javascript
var $ = require('jm-core');
var module1 = require('./module1');

//加载
var jm = $()
        .use(module1)
    ;

// 使用加载的模块
jm.logger.debug(jm.module1.toString());

//卸载
jm.unuse ('module1');
```

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

父类 jm.Class 。

Object#attr 批量设置对象属性。

```javascript
var obj = jm.object();
obj.attr(
    {
        name: 'test',
        value: 123
    }
);
console.info(obj);
```

## 事件 EventEmitter
### EventEmitter 简介

父类 jm.Object 。

EventEmitter 的核心就是事件触发与事件监听器功能的封装。

下面我们用一个简单的例子说明 EventEmitter 的用法：

```javascript
var emitter = jm.eventEmitter();
//或者var emitter = new jm.EventEmitter()
emitter.on('some_event', function() {
	console.log('some_event 事件触发');
});
setTimeout(function() {
	emitter.emit('some_event');
}, 1000);
```

执行结果如下：

运行这段代码，1 秒后控制台输出了 'some_event 事件触发'。 其原理是 event 对象注册了事件 some_event 的一个监听器，然后我们通过 setTimeout 在 1000 毫秒以后向 event 对象发送事件 some_event，此时会调用some_event 的监听器。

EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件，EventEmitter 支持 若干个事件监听器。

当事件触发时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。

让我们以下面的例子解释这个过程：

```javascript
var emitter = jm.eventEmitter();
emitter.on('someEvent', function(arg1, arg2) {
	console.log('listener1', arg1, arg2);
});
emitter.on('someEvent', function(arg1, arg2) {
	console.log('listener2', arg1, arg2);
});
emitter.emit('someEvent', 'arg1 参数', 'arg2 参数');
```

执行以上代码，运行的结果如下：

```javascript
listener1 arg1 参数 arg2 参数
listener2 arg1 参数 arg2 参数
```

以上例子中，emitter 为事件 someEvent 注册了两个事件监听器，然后触发了 someEvent 事件。

运行结果中可以看到两个事件监听器回调函数被先后调用。 这就是EventEmitter最简单的用法。

EventEmitter 提供了多个属性，如 on 和 emit。on 函数用于绑定事件函数，emit 属性用于触发一个事件。

### EventEmitter#on(name, fn, caller)

为指定事件注册一个监听器，接受一个字符串 name 、一个回调函数 fn 和回调函数调用主体 caller（可选）。

```javascript
server.on('connection', function (stream) {
  console.log('someone connected!');
});
```

### EventEmitter#once(name, fn, caller)

为指定事件注册一个单次监听器，即 监听器最多只会触发一次，触发后立刻解除该监听器。

```javascript
server.once('connection', function (stream) {
  console.log('Ah, we have our first user!');
});
```

### EventEmitter#removeListener(name, fn, caller)

移除指定事件的某个监听器，监听器 必须是该事件已经注册过的监听器。

```javascript
var callback = function(stream) {
  console.log('someone connected!');
};
server.on('connection', callback);
// ...
server.removeListener('connection', callback);
```

### EventEmitter#removeAllListeners(name)

移除所有事件的所有监听器， 如果指定事件，则移除指定事件的所有监听器。

### EventEmitter#listeners(name)

返回指定事件的监听器数组。

### EventEmitter#emit(name, arg1, arg2, arg3, arg4, arg5)

按参数的顺序执行每个监听器。

## 标签对象 TagObject
## 随机数 Random
