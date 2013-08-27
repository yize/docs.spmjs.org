# spm-init

- pubdate: 2013-08-07
- category: 通用插件
- index: 10

-----------

## 安装

```
npm install spm -g
npm install spm-init -g
```

安装模板需要 git，确保能在命令行里运行 git。

## 使用说明

可以根据一个指定的模板初始化当前目录，但首先需要[安装模板](#安装模板)。

```
spm init arale
```

arale 为模板(aralejs/template-arale)的别名，安装模板时会生成，一般为"-"之后的字符。已下载的模块可通过 `spm init -h` 查看。

### 模板存放路径

模板文件默认路径为 `~/.spm/init`，可以通过配置（`~/.spm/spmrc`）添加

```
[init]
template = ~/.spm-init
```

或执行

```
$ spm config init.template ~/.spm-init
```

### 安装模板

模板是从 github 上抓取的，可以是任何公开仓库，如 https://github.com/aralejs/template-arale/ ，下载时可执行以下命令，模板会下载到上面提到的路径。

```
$ spm-init -i aralejs/template-arale
```

### 自定义模板

spm-init 完全兼容 grunt-init，所以你可以用 [grunt 的模板](http://gruntjs.com/project-scaffolding#installing-templates)。

自定义模板可参照 [grunt 文档](http://gruntjs.com/project-scaffolding#custom-templates)

## 选项

### -i, --install

安装模板

```
$ spm-init --install aralejs/template-arale.git

// 使用 index.json 中的别名
$ spm-init --install arale
```

### -u, --upgrade


更新模板，会执行 `git pull`

```
$ spm-init --upgrade arale
```

### -l, --list

显示 [index.json](https://github.com/spmjs/spm-init/blob/master/index.json) 中的所有模板

```
$ spm-init --list
```

### --update


从服务器获取模板索引 index.json

```
$ spm-init --upgrade arale
```
  
###  -f, --force

当前目录存在文件仍然继续执行。
