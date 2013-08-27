# spm-test

- pubdate: 2013-08-08

-----------

## 安装

```
npm install spm -g
npm install apm -g
npm install jscoverage -g
npm install mocha-browser -g
npm install phantomjs -g
```

## 使用说明

> 此工具只支持支付宝内部使用

spm test 使用 phantomjs 跑测试用例，测试 src 和 dist 代码，并使用 jscoverage 生成覆盖率文档。 

**需要使用 [nico-arale](https://github.com/aralejs/nico-arale/) 作为文档模板，并用 spm doc 生成本地测试文档先。**