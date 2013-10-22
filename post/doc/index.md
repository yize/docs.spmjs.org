# 新手入门

- pubdate: 2013-08-15
- category: 新手入门
- index: 1

---

spm 是 CMD 的包管理工具，需要和 SeaJS 配合使用。使用前请先阅读一下 [SeaJS 的官方文档](http://seajs.org/)，确保已经了解 SeaJS 及其使用方式。

## 安装和配置

安装 spm，在此之前请先[配置 Node 环境](./environment.html)

```
$ npm install spm -g
```

spm 核心只有包管理功能，除此之外还提供了很多[插件](../cli/help.html)。

配置[源服务](https://spmjs.org/)，在源服务上可以找到所有人分享的模块。

```
$ spm config source:default https://spmjs.org
```

## 模块

spm 并没有限制模块的目录结构和组织方式，但是会有推荐的方式，可以先看下[标准模块](https://github.com/spmjs/spm-build/tree/master/examples/simple)和[自定义模块](https://github.com/spmjs/spm-build/tree/master/examples/simple-grunt)的示例。

虽然模块的组织方式不同，但上线前都需要做 [transport](./transport.html) 处理，所以 spm 还提供了构建工具，也分为[标准构建](./spm-build.html)和[自定义构建](./grunt-build.html)两种。


## 插件

spm 还提供一些插件，也欢迎更多插件开发者，[如何开发?](../api/develop-plugin.html)。

- [spm-build](../cli/build.html) 构建工具
- [spm-init](../cli/init.html) 初始化模块
- [spm-status](../cli/status.html) 检查线上 http 状态

## 基本命令的使用视频

<iframe src="http://ascii.io/a/2533/raw" frameborder="0" width="566" height="646"></iframe>



## 贡献

我们非常欢迎加入我们的大家庭，一起来维护 spm，[如何贡献?](./contribute.html)
