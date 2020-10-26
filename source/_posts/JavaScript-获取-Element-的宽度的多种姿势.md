---
title: JavaScript 获取 Element 的宽度的多种姿势
date: 2020-10-26 22:20:39
copyright: true
abstract: 最近在写一个小组件，涉及到获取 Element 的宽度，就顺便整理了一些。
categories:
- [计算机技术]
tags:
- 前端
- javascript
---
# JavaScript 获取 Element 的宽度的多种姿势

最近在写一个小组件，涉及到获取 Element 的宽度，就顺便整理了一些

## clientWidth & offsetWidth

如果 Element 的宽度是写在 css 文件中的，比较常见的方法就是通过 [HTMLElement.clientWidth](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/clientWidth) 和 [HTMLElement.offsetWidth](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetWidth) 来获得。

两则的区别很明显: 

- 前者得到的宽度是 `内容区宽度 + padding `
- 后者得到的宽度是 `内容区宽度 + padding + border + margin`

但是如果元素添加了 `display: none` 的样式， 那么上面两种方法得到的值都会是 `0`

## 那要怎么获得隐藏起来的元素的宽度？

虽然上述的两种方式不适用于 `display：none` 的情况，但是适用于 `visibility：hidden` 的情况。

如果想获取 `display: none` 元素的宽度，目前我是用一下两种方式的：

- 第一种，元素的宽度用内联样式定义，然后通过 `HTMLElement.style.width` 获得宽度
- 第二种，通过 [window.getComputedStyle()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/getComputedStyle) 来获得
  - `window.getComputedStyle(target).width`，需要注意的是，得到的宽度是一个字符串，例如 `100PX`
  - 获得的宽度值会受 `box-sizing` 样式的影响
  - 无论是宽度是内联样式定义的还是外联样式定义的，都可以获取到

个人非常喜欢第二种方式，目前看来在各种情况下都能拿到我想要的宽度！