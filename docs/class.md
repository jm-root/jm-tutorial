# 类 Class
[jm-class] (https://github.com/jm-root/jm-class)

- 引入
- 类的定义
- 类的继承
- 类的保留属性

## 引入
install：

```javascript
npm install --save jm-class
```

ES6：

```javascript
import Class from 'jm-class';
let o = new Class();

```

node：

```javascript
var Class = require('jm-class');
let o = new Class();

//也可以采用全局变量jm，不推荐
require('jm-class');
let o = new jm.Class();

```

browser：

```
<script src="dist/js/jm-core.js"></script>
<script src="dist/js/jm-class.js"></script>
```
## 类的定义
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

## 类的继承

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

## 类的保留属性

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
