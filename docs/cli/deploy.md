# spm-deploy

- pubdate: 2013-08-08

-----------

## 安装

```
npm install spm -g
npm install spm-deploy -g
```

## 使用说明

> 此命令只能在支付宝内部使用，外部需要自己写 Gruntfile

通过 scp 把模块上传到服务器上，服务器要支持 ssh，默认用户名密码为 admin/alipaydev。

默认上传到 assets.dev.alipay.net

```
$ cd widget
$ spm deploy
```

上传后可访问 http://assets.dev.alipay.net/arale/widget/1.0.0/widget.js

## 选项

### --target


可指定坑位，如 p11，也就是上传到 assets.p11.alipay.net

```
$ spm deploy --target p11
```

### --host


可指定域名

```
$ spm deploy --host assets.a1.alipay.net
```

### --username

可指定用户名

### --password

可指定密码
