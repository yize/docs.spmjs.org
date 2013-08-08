# spm-zip

- pubdate: 2013-08-08

-----------

## 安装

```
npm install spm -g
npm install apm -g
```

## 使用说明

将模块打成 zip 包，包内以 `family/name/version` 的方式存放。

```
$ cd widget
$ spm zip
```

还可以直接打包源上已有的文件

```
$ spm zip arale/widget
$ spm zip arale/widget@1.0.0
```

## 选项

### -s, --source

指定源，详情看[配置文档]()。

### -I, --input

zip 是将 dist 下的文件打包，input 选项可指定其他目录

### -O, --output

ouput 选项可指定输出的文件名
    
### --format

可指定压缩包内的路径，默认为 `family/name/version`