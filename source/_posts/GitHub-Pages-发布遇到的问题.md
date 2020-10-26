---
title: GitHub Pages 发布遇到的问题
date: 2020-10-26 21:20:14
copyright: false
header_image: /intro/git_header.png
abstract: 将包发不到 github pages 时遇到的问题
categories:
- [计算机技术]
tags:
- Git
- 搬运
---

## GitHub Packages 的发布

> 参考这篇[文章](https://blog.csdn.net/yehuozhili/article/details/106632786)，并补充一部分自己实际操作中发现的内容

## 关于文件名称

假设要发布的这个包叫 `mypackages`， 然后我们 GitHub 的用户名为 `myname`，那么 `package.json` 中`name` 属性的值就会是 `@myname/mypackages`

## 关于登录命令

参考文章中说需要执行这样的代码进行登录：

```bash
npm login --registry=https://npm.pkg.github.com --scope=@trcat
```

但我们如果按照前面设定好包的名称，登录命令直接用下面这个就可以了

```bash
npm login --registry=https://npm.pkg.github.com
```

## 其他

目前不知道为啥，虽然看上去 github 和 npm 有联动，但实际上，发布到 github 上的包在 npm 中是搜不到的。
