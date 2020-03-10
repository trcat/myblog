---
title: React Native 文档基础部分小结
date: 2020-03-10 19:52:25
copyright: true
abstract: 看 React Native 官方文档顺手记录的注意点。
categories:
- [计算机技术]
tags:
- react-native
---

非常鼓励看原文文档，目前文档内容特别完善。以下是我在看文档的**基础部分**的时候顺手记录的内容。




## 使用的脚手架

官方文档提示有两种选择

- expo cli
- react native cli

虽然 expo cli 的安装上比较麻烦，但是从开发的角度来看，expo cli 方便很多，在手机上的预览完全可以依靠 Expo App 来实现，完全不需要再在电脑上下载模拟器。



## React Native Component

React 没有自己的元件，但是 React Native 有，借助这些基础元件帮助我们实现快速开发，实现网页端和手机端的互通。



## Style

React Native 对这部分内容有扩充：

- 新增了 `StyleSheet.create`，方便对组件样式的统一管理
  - 其中 key 的名字参考 css 的样式名，只不过要修改成驼峰型，value 参照 css 的值。
- React Native 基础组件都有 `style` prop，用来设定组件的样式
  - 这个 prop 的值可以是 Object，也可以是一个 Array。如果是 Array，越靠后的样式级别越高。



```javascript
import React, { Component } from 'react';
import { StyleSheet, Text, View } from 'react-native';

const styles = StyleSheet.create({
  bigBlue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigBlue}>just bigBlue</Text>
        <Text style={[styles.bigBlue, styles.red]}>bigBlue, then red</Text>
        <Text style={[styles.red, styles.bigBlue]}>red, then bigBlue</Text>
      </View>
    );
  }
}

```



## Height and Width

主要介绍两种方式来设定组件的大小，知道 css 的话这部分内容就很好理解：

- 设定固定值：
  - 设定 `style` 的 `width` 和 `height`
- 动态设定：
  - 用 `flex`  进行设定



## Layout with Flexbox

主要详细说明 `flex` 的相关设定，知道 css 的 `flex` 的话这部分内容就很好理解。主要区别如下：

- React Native 中的 `flexDirection` 默认为 `column` 
- React Native 中的 `flex` 只能接受一个数字作为其值



这里还介绍了 `width` 和 `height` 的值的类型（和 传统 css 有出入）

- auto
  - 默认值
- 像素
- 百分数



这里还介绍了 `position` 的值（和传统 css 有出入）

- absolute
- relative
  - 默认值。这里需要注意，传统的 css，`staitc` 才是默认值