# SPM 全局配置

- pubdate: 2013-09-10
- category: 规范标准
- index: 5

----------

安装好 SPM 之后, 会在用户目录下生成 `.spm` 目录, 里面包含了各种各样的信息, 在此说明下各个文件/目录的含义.

```
.spm
| -- spmrc
| -- deps.json
| -- plugins.json
| -- run.json
| -- init/
| -- themes/
| -- src/
| -- cache/
```

## spmrc

见 [spmrc 文档](/doc/spmrc)

## run.json

用于统计 SPM 各个命令执行了多少次和最后执行时间.

## deps.json

存储当前 SPM 依赖的各个模块的版本号, 以便在 `spm check` 时查找依赖更新.

## plugins.json

存储当前安装的所有 SPM 插件.

## init/

存放不同类型模块的模板文件, 主要用于 `spm init xxx` 时, 从 init/xxx 目录获取配置及模板文件来拷贝.

每个目录其实是克隆了 https://github.com/spmjs 下 template-xxx 仓库, 所以可以直接 git pull 操作.

## themes/

文档生成时使用的不同主题, 目前两套 arale 和 alice.

arale 克隆的是 https://github.com/aralejs/nico-arale 仓库, alice 克隆的是 https://github.com/aliceui/nico-alice 仓库.

## src/

## cache/

`spm install` 时临时缓存的模块目录.