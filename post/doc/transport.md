# transport

- pubdate: 2013-08-15
- category: 规范标准
- index: 5

----------

## transport 是什么？

根据 [CMD 的模块定义规范](https://github.com/seajs/seajs/issues/242) 可以定义如下模块

```
define(function(require, exports, module) {
  var Base = require('base');
  var Widget = Base.extend({
    ...
  });
  module.exports = Widget;
})
```

但这样写在线上运行会有一些问题

1. 无法在一个文件中定义多个模块，

    这个问题在 combo 中尤为明显，多个 js 文件被动态合并成一个文件下载下来。

    ```
    // a.js
    define(function(){});
    // b.js
    define(function(){});
    // c.js
    define(function(){});

    // a.js,b.js,c.js
    define(function(){});
    define(function(){});
    define(function(){});
    ```

    因为模块是跟 url 一一对应的，所以合并后无法匹配相应的模块了。这个问题可以用添加 id 的方式解决。

2. 需要分析代码解析依赖

    seajs 是通过分析 factory 的源码进行依赖分析的，提取所有的 require 即所有的依赖。但是在线上运行这一步是非常耗性能的，可以在构建的时候提前提取依赖。

所以最后上线的模块应该是 define(id, deps, factory) 这种形式的，对原始的模块进行的转换我们称之为 transport。

## id 规范

Transport 后每个模块的标识为 idleading + 文件名，idleading 的格式是 `family/name/version`。

```
// base.js
define(function(){});

// transport 后的 base.js
define('arale/base/1.0.0/base', ['arale/class/1.0.0/class','arale/events/1.0.0/events','./aspect','./attribute'], function(){});
```

这个 id 会在多处使用

1. 物理存放路径/URL

    上面 base.js 的访问路径为 http://assets.spmjs.org/arale/base/1.0.1/base.js

2. 模块的 id

   define 的 id 必须为这个，而且需要跟 url 匹配。

   具体如何匹配是根据 seajs 而定的，一般 seajs 会放在根目录(`/sea.js` `/seajs/sea.js` `/seajs/seajs/2.1.1/sea.js` 都可以)，所以 base 就为 http://assets.spmjs.org 。

   “请求的 url” = “seajs 的 base” + “define 的 id”

3. 包的 id

    通过 spm 管理模块包，也需要定义 family，name 和 version。
    