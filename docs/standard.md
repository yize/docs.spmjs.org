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

spm follows the [Common Module Definition](https://github.com/spmjs/specification) packaging standards, compatible with nodejs' package.json.

CMD [packaging draft](https://github.com/spmjs/specification/blob/master/draft/package.md) add an additional namespace, which is `family`. spm add another namespace, which is `spm`.

Here is an example of `package.json`:

```
{
    "family": "arale",
    "name": "base",
    "version": "1.0.0",
    "description": "base is ....",
    "homepage": "http://aralejs.org/base/",
    "repository": {
        "type": "git",
        "url": "https://github.com/aralejs/base.git"
    },
    "keywords": ["class"],

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


## family

This is the account name on http://spmjs.org.

## name

This is your package's name.

## version

The version of your package. We only accept version like this:

```
1.0.0
```

The regexp is `\d+\.\d+\.\d+`.

## description

Put a description in it. It's a string. This helps people discover your package, as it's listed in `spm search`.


## keywords

Put keywords in it. It's an array of strings. This helps people discover your package as it's listed in `spm search`.

## homepage

The url to the project homepage.

## repository

The repository of your project.

## private

If you set `"private": true` in your package.json, then spm will refuse to publish it to https://spmjs.org.

This is a way to prevent accidental publication of private repositories. But you can publish to other source center.

## spm.alias

Alias.

## spm.output

Output is an array that contains the files for distribution, it will auto concat the relative dependencies.

### Single File

For example:

```js
// a.js
define(function(require) {
    require('./b')
});

// b.js
define(function(require) {
    require('./c')
});

// c.js
define(function(require) {
});
```

Now define your output as:

```json
{
    "output": ["a.js", "c.js"]
}
```

It will create a `a.js` and a `c.js` in the `dist` directory. The `dist/a.js` contains code of `src/a.js`, `src/b.js` and `src/c.js`. The `dist/c.js` will only contain the code of `src/c.js`, because it requires nothing.


### Glob Pattern

Output also support glob patterns. Take an example:

```
package.json
src/
    i18n/
        en.js
        zh.js
        fr.js
```

Now define your output as:

```json
{
    "output": ["i18n/*.js"]
}
```

And it will distribute every js files to `dist` folder.

If your folder structure is something like this:

```
src/
    i18n/
        locale.js
        en/
            locale.js
        zh/
            zh_CN/
                locale.js
            zh_TW/
                locale.js
```

You should define your output as:

```json
{
    "output": ["i18n/**/*"]
}
```

## spm.include

This means the build strategy, options for include:

- relative: this is the default value, include relative dependencies
- all: include all dependencies
- self: include only my self


## Old Time

1. `root` is deprecated, use `family` instead.
2. `dependencies` is deprecated, use `spm.alias` instead.
3. `output` changed
