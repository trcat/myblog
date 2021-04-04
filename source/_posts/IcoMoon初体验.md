---
title: IcoMoon初体验
date: 2020-12-28 20:41:08
copyright: true
abstract: 前几天工作上看到前同事用这个，简单的了解了一下。
categories:
- [计算机技术]
tags:
- 前端
- SVG
- WebFont
- 工具
---
# IcoMoon

[icoMoon工具网址](https://icomoon.io/app/#/select)

这是一个可以将 SVG 格式的文件转换为 web font （即使用字体显示图标）的神奇网站工具，工具的使用非常简单，基本操作如下图所示：

![icomoon_useage](icomoon_useage.png)



## 优势

使用 web font 的形式来显示图标最大的优势就是，若要修改图标的颜色，只需要调整 css `color` 的值就可以了：

```css
.icon1 {color:black;} // 图标会变成黑色
.icon2 {color:red;} // 图标会变成红色
```



## 唯一且最大的难点

icoMoon 工具使用起来非常非常的简单，唯一且最大的难点，就是 svg 文件的取得。

一般情况下，我们前端从设计师的 psd 文件中切图后，得到的图标都是 png 格式的，所以我们要想办法将 png 格式转换成 svg 格式。

很不幸，目前我并没有十全十美的转换方案，稍微复杂一些的 png 转换成 svg 后，要么 icoMoon 工具无法识别，要么就是转换后图标面目全非，就像下面两张图所示，图1为转换前，图2为转换后：

![icon1](icon1.png)-------png转换为svg------------>![icon2](icon2.png)

但是相对简单的图像问题就不是很大:

<img src="icon2-1.png" alt="icon2-1" style="zoom:25%;" />--------简单图片差别就不大--------------<img src="icon2-2.png" alt="icon2-2" style="zoom:25%;" />

所以还算有一线生机，这边还是有必要说下目前可行的 png 转 svg 的流程

### 转换流程

1. 用 ps 的切图功能切下想要的图标，并保存为 png 格式，
2. 然后用这个 [在线工具](https://convertio.co/zh/) 将 png 转换成 svg，并下载。


