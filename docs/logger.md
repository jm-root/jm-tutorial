# 日志 Logger
[jm-logger] (https://github.com/jm-root/jm-logger)

- 引入
- 日志 logger

## 引入

- install

```javascript
npm install --save jm-logger
```

- ES6

```javascript
import log from 'jm-logger';
let logger = log.logger;
//或者
let logger = log.getLogger('main');

```

- node

```javascript
var log = require('jm-logger');
var logger = log.logger;
//或者
var logger = log.getLogger('main');

```

- browser

```
<script src="dist/js/jm-logger.js"></script>
<script>
    var logger = jm.logger;
    //或者
    var logger = jm.getLogger('main');
</script>
```
## 日志 logger

```javascript
var log = require('jm-logger');
//默认日志
var logger = log.logger;
['trace','debug','info','warn','error','fatal'].forEach(function(level) {
    logger[level]('logger test: %s %s', level, Date.now());
});

//分类日志
var logger = log.getLogger('main');
['trace','debug','info','warn','error','fatal'].forEach(function(level) {
    logger[level]('logger test: %s %s', level, Date.now());
});
```
