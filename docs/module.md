# 模块 Module
[jm-module] (https://github.com/jm-root/jm-module)

- 引入
- 模块化设计
- 模块的定义
- 模块的加载、使用和卸载

## 引入

- install

```javascript
npm install --save jm-module
```

- ES6

```javascript
import mdl from 'jm-module';

let root = {};
mdl.enableModule(root);

//或者
class Root {
    constructor() {
        mdl.enableModule(this);
    }
}
```

- node

```javascript
var mdl = require('jm-module');

var root = {};
mdl.enableModule(root);

```

- browser

```
<script src="dist/js/jm-module.js"></script>
<script>
    var root = {};
    jm.enableModule(root);
</script>
```

## 模块化设计

为了方便扩展， jm 采用了模块化设计理念，一切都是模块。

模块可以动态加载和卸载。

## 模块的定义

ES6：

```javascript
// module1.js
export default function (name = 'module1') {
    var $ = this;
    $[name] = {
        toString: () => {
            return 'this is a module';
        }
    };
    return {
        name: name,
        unuse: () => {
            delete $[name];
        }
    };
};
```

node：

```javascript
// module1.js
module.exports = function (name) {
    var $ = this;
    name || (name = 'module1');
    $[name] = {
        toString: function () {
            return 'this is a module';
        }
    };
    return {
        name: name,
        unuse: function () {
            delete $[name];
        }
    };
};
```

## 模块的加载、使用和卸载

ES6：

```javascript
import mdl from 'jm-module';
import module1 from './module1';

let root = {};
mdl.enableModule(root);

//加载
root.use(module1);

// 使用加载的模块
root.module1.toString();

//卸载
root.unuse ('module1');

```

node：

```javascript
var mdl = require('jm-module');
var module1 = require('./module1');

let root = {};
mdl.enableModule(root);

//加载
root.use(module1);

// 使用加载的模块
root.module1.toString();

//卸载
root.unuse ('module1');

```
