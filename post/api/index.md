# 总述

- pubdate: 2013-03-26
- category: 高层 API
- index: 0

-----------

spm 的 API 说明.

-----------

## 关系

todo: spm, grunt, yuan 的关系.

## 如何引入?

spm 是一个标准 nodejs 模块, 所以在安装好 spm 之后, 只需要通过 `require` 就可引入 spm 这个模块.

```js
var spm = require('spm')
```

## 查看当前版本

`spm.version` 中包含 spm 的版本信息.

```
> spm.version
'2.1.11'
```

