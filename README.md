# modular-specification
深入理解常见模块化规范，如CJS、AMD、UMD、ESM、IIFE等。

## cjs
### 1. 说明
1. 每个js文件都可当作一个模块，并且自身存在module对象
2. 在服务器端：模块的加载是运行时同步加载的
3. 在浏览器端：模块需要提前编译打包处理
4. require('./demo.js') 只要出现require就会执行demo.js内的代码
5. 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存

### 2. 语法
```js
module.exports = value
exports.xxx = value
// 两者暴露的本质都是exports对象
```
初始时，两者关系是module.exports = exports = {}，require所接收到的是modules.exports指向的对象。

demo案例：
```js
module.exports = 1
exports.a = 2

const mo = require('./mo.js')
console.log(mo)   // 1 
------------------------------------
module.exports = 1
module.exports = 2

const mo = require('./mo.js')
console.log(mo)   // 2
------------------------------------
module.exports = 1
module.exports.a = 2

const mo = require('./mo.js')
console.log(mo)   // 1
------------------------------------
module.exports = {a: 2}
module.exports.b = 2

const mo = require('./mo.js')
console.log(mo)   // {a: 2, b: 2}
------------------------------------
module.exports = {a: 2}
exports.b = 2

const mo = require('./mo.js')
console.log(mo)   // {a: 2}
------------------------------------
exports.a = 1
exports.b = 2

const mo = require('./mo.js')
console.log(mo)   // {a: 1, b:2}
```

## amd（Asynchronous Module Definition）
https://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html

## cmd（Common Module Definition）
RequireJS(实现amd的js库) 与 SeaJS(实现cmd的js库) 的异同
https://github.com/seajs/seajs/issues/277
AMD 和 CMD 的区别有哪些？
http://www.zhihu.com/question/20351507/answer/14859415

## umd（Universal Module Definition）
同时兼容AMD和CommonJS规范而出现的。

## esm
https://hacks.mozilla.org/2015/08/es6-in-depth-modules

## IIFE（iImmediately Invoked Function Expression）
