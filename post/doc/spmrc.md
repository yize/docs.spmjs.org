# spmrc

- pubdate: 2013-08-15
- category: 规范标准
- index: 2

----------

spmrc 为 spm 及其插件所使用的配置文件，文件为 `~/.spm/spmrc`，可通过[类库](https://github.com/spmjs/spmrc)和 [spm config]() 进行操作。

spmrc 是以 ini 形式存储的，结构如下

```
[section1]
name = property

[section2]
name = property
```

以下会列举一些全局的配置

## user

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

## source

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
