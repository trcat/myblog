---
title: 如何判断当前页面是否被 iframe 标签引用
date: 2020-10-28 22:17:55
copyright: false
abstract: 防止其他网站用 iframe 标签引入自己的页面。
categories:
- [计算机技术]
tags:
- html
- javascript
- 转载
---

> [参考文档](https://www.jb51.net/article/102711.htm)

只需要比对`window.top` 和 `window.self` 是否一样，如果一样，则说明没有被引用，反之则说明被引用了。

实例代码如下：

```javascript
if (window.top !== window.self) {
    // 当前被 iframe 引用了
}
```




