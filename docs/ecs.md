# 实体组件系统 ECS
[jm-ecs] (https://github.com/jm-root/jm-ecs)

- 引入
- 实体组件系统 ECS
- 实体管理器 EntityManager
- 实体 Entity
- 组件 Component
- 工厂 Factory
- 处理器 Processor

## 引入
install：

```javascript
npm install --save jm-ecs
```

ES6：

```javascript
import ECS from 'jm-ecs';
let ecs = new ECS();

```

node：

```javascript
var ECS = require('jm-ecs');
var ecs = new ECS();

//也可以采用全局变量jm，不推荐
require('jm-ecs');
var ecs = jm.ecs();

```

browser：

```
<script src="dist/js/jm-ecs.js"></script>
```

## 实体组件系统 ECS
## 实体管理器 EntityManager
node：

```javascript
var em = ecs.em();

```
## 实体 Entity
node：

```javascript
var e = em.e('type', opts);

```
## 组件 Component
## 工厂 Factory
## 处理器 Processor
