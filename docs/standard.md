# 配置规范

- pubdate: 2013-08-15
- index: 5

----------

## spmrc

spmrc 为 spm 及其插件所使用的配置文件，文件为 `~/.spm/spmrc`，可通过[类库](https://github.com/spmjs/spmrc)和 [spm config]() 进行操作。

spmrc 是以 ini 形式存储的，结构如下

```
[section1]
name = property

[section2]
name = property
```

以下会列举一些全局的配置

### user

可指定一个 gruntfile 的路径，可以配置本地或远程的。

```
[user]
gruntfile =
```

通过 gruntfile 可高度自定义，如

1. 自定义命令

    在 gruntfile 注册一个 task hello，就可以用 spm hello 执行。

2. 覆盖原有命令

    在 gruntfile 重置下 build 的任务，可参考 [apm](https://github.com/spmjs/apm/blob/master/Gruntfile.js)。

### source

用 source 来指定源，可以指定多个。

```
[source:default]
url = http://spmjs.org
auth =

[source:alipay]
url = http://spmjs.alipay.com
```

然后可以通过 -s 指定，使用 default 可不指定，如将模块上传到 alipay 的源

```
spm publish -s alipay
```

任何人都可以从源读取，但是**写操作是要登录的**。先到源上注册账号通过 [spm login]() 登录，配置文件中会生成一个 auth 的 token。

可支持代理

```
[source:default]
url = http://spmjs.org
proxy = username:password@proxy.server:port
```

## package.json

spm 遵循 [Common Module Definition](https://github.com/spmjs/specification) 的 [packaging draft](https://github.com/spmjs/specification/blob/master/draft/package.md) 规范，每个模块必须有一个 package.json 文件来描述模块自身。

以下为 package.json 的示例

```
{
    "family": "arale",
    "name": "base",
    "version": "1.0.0",
    "description": "base is ....",
    "keywords": ["class"],
    "author": "Hsiaoming Yang <me@lepture.com>",
    "maintainer": [
    	"Hsiaoming Yang <me@lepture.com>",
    	"Haoliang Gao <a@chuo.me>"
    ],
    "homepage": "http://aralejs.org/base/",
    "repository": {
       	"type": "git",
        "url": "https://github.com/aralejs/base.git"
    },
    "bugs": {
        "url": "https://github.com/arale/overlay/issues"
    },

    "spm": {
        "source": "src",
        "output": ["base.js", "i18n/*"],
        "alias": {
            "class": "arale/class/1.0.0/class",
            "events": "arale/events/1.0.0/events"
        }
    }
}
```

对于 spm 来说 family、name 和 version 三个字段是必须的；package.json 中的 spm 字段是扩展字段，供 spm build 使用。


## family `required`

这个字段为源 (http://spmjs.org) 上的账户名，可指定一类模块，我们称之为「家族」。这个字段存在的原因是为了解决命名冲突的问题，灵感来源于 github。

世界这么大，不同的人开发同名组件是很常有的事情，像 arale/events 和 popomore/events 可以并存。

此外还能将一种类型的模块都放在一个 family 下，如 jquery 以及他的 ui 组件都可以放在 jquery 的 family 下。

命名规范支持小写字母，数字和 -，正则匹配 `[a-z0-9-]`。

## name `required`

模块的名字，命名规范同 family。

## version `required`

版本使用 `MAJOR.MINOR.PATCH` 版本好，正则匹配 `\d+\.\d+\.\d+`。

PATCH 变更为 bugfix，MINOR 为非兼容的修改和功能新增，MAJOR 为定位调整或大范围的重写。

## description

模块的简介，对模块的描述应该能让其他人了解模块的功能，可通过 spm search 搜索。

## keywords

模块的关键字，为一个数组，可通过 spm search 搜索。

## author

模块的作者，也就是最初开发这个模块的人。

支持两种写法

```
"author": "Hsiaoming Yang <me@lepture.com>"

"author": {
	"name": "Hsiaoming Yang",
	"email": "me@lepture.com"
}
```

## maintainer

后期模块的维护者或贡献者，为一个数组。

## homepage

模块的文档页面。

## repository

模块的仓库。

## bugs

模块问题和讨论的链接。

## private

If you set `"private": true` in your package.json, then spm will refuse to publish it to https://spmjs.org.

This is a way to prevent accidental publication of private repositories. But you can publish to other source center.

## spm

这个字段是供 spm build 使用，请看[构建章节]()。

