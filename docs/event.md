# 事件 Event
[jm-event] (https://github.com/jm-root/jm-event)

- 引入
- EventEmitter 简介
- EventEmitter#on(eventName, fn, prepend)
- EventEmitter#once(eventName, fn, prepend)
- EventEmitter#off(eventName, fn)
- EventEmitter#listeners(eventName)
- EventEmitter#emit(eventName, arg1, arg2, arg3, arg4, arg5)

## 引入

- install

```javascript
npm install --save jm-event
```

- ES6

```javascript
import event from 'jm-event';
let emitter = {};
event.enableEvent(emitter);

```

- node

```javascript
var event = require('jm-event');
var emitter = {};
event.enableEvent(emitter);

```

- browser

```
<script src="dist/js/jm-event.js"></script>
<script>
    var emitter = {};
    jm.enableEvent(emitter);
</script>
```
## EventEmitter 简介

EventEmitter 的核心就是事件触发与事件监听器功能的封装。

```javascript
var event = require('jm-event');
var emitter = {};
event.enableEvent(emitter);
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
var event = require('jm-event');
var emitter = {};
event.enableEvent(emitter);
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

## EventEmitter#on(eventName, fn, prepend)

为指定事件注册一个监听器。

```javascript
server.on('connection', function (stream) {
  console.log('someone connected!');
});
```

## EventEmitter#once(eventName, fn, prepend)

为指定事件注册一个单次监听器，即 监听器最多只会触发一次，触发后立刻解除该监听器。

```javascript
server.once('connection', function (stream) {
  console.log('Ah, we have our first user!');
});
```

## EventEmitter#off(eventName, fn)

移除指定事件的某个监听器。

如果未指定fn，则移除指定事件的所有监听器。

如果未指定事件，则移除所有监听器。

```javascript
var callback = function(stream) {
  console.log('someone connected!');
};
server.on('connection', callback);
// ...
server.off('connection', callback);
```

## EventEmitter#listeners(eventName)

返回指定事件的监听器数组。

## EventEmitter#emit(eventName, arg1, arg2, arg3, arg4, arg5)

按顺序执行每个监听器。
