# 错误 Err
[jm-err] (https://github.com/jm-root/jm-err)

- 引入
- 错误定义

## 引入

- install

```javascript
npm install --save jm-err
```

- ES6

```javascript
import error from 'jm-err';
let Err = error.Err;
```

- node

```javascript
var error = require('jm-err');
var Err = error.Err;
```

- browser

```
<script src="dist/js/jm-err.js"></script>
<script>
    var Err = jm.Err;
</script>
```

## 错误定义

Err 统一定义了常用的错误，格式如下，其中 err 表示错误的编码，msg 表示错误的信息。

```javascript
Err = {
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
|FA_NOTEXISTS|9|Not Exists|
|FA_EXISTS|10|Already Exists|
|OK|200|OK|
|FA_BADREQUEST|400|Bad Request|
|FA_NOAUTH|401|Unauthorized|
|FA_NOPERMISSION|403|Forbidden|
|FA_NOTFOUND|404|Not Found|
|FA_INTERNALERROR|500|Internal Server Error|
|FA_UNAVAILABLE|503|Service Unavailable|
