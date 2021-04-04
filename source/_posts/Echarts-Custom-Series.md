---
title: Echarts Custom Series
date: 2021-04-04 22:56:38
copyright: true
abstract: 工作上遇到需要使用自定义系列的需求，故在这边记录一下
categories:
- [计算机技术]
tags:
- 前端
- echarts
---
# Echarts Custom series

工作上一直都有在用 Echarts，但是基本上都是使用 Echarts 预设好的 series，例如 `bar`、`line`、`pie`，然而最近因为工作需要，尝试使用了 `custom` 自定义图表，有必要记录一下。

## renderItem

`custom` series 大致设定上与其他 series 区别不大，详情可看[配置项文档](https://echarts.apache.org/zh/option.html#series-custom)，最关键的设定就是 [`renderItem`](https://echarts.apache.org/zh/option.html#series-custom.renderItem)，全靠它实现我们的自定义图像渲染逻辑。

 `renderItem` 是一个函数，**依据传入 series 的 data ，遍历并返回对应的渲染逻辑**，它包含 [`params`](https://echarts.apache.org/zh/option.html#series-custom.renderItem.arguments.params) 和 [`api`](https://echarts.apache.org/zh/option.html#series-custom.renderItem.arguments.api) 这两个参数，需要**当前数据属性**和**坐标系属性**就从 `params` 中拿，需要**获取当前数据维度值或将数据映射到坐标系中**就从`api` 中拿对应的函数。

如官方配置项文档所说，[`api.coord`](https://echarts.apache.org/zh/option.html#series-custom.renderItem.arguments.api.coord) 和 [`api.size`](https://echarts.apache.org/zh/option.html#series-custom.renderItem.arguments.api.size)  这两个函数很常用，前者传入数据得到**对应映射到坐标系的坐标点**，后者传入数据得到**对应映射到坐标系的长度**，当然还有 [`api.value`](https://echarts.apache.org/zh/option.html#series-custom.renderItem.arguments.api.value) ，可以通过这个拿到当前数据`value`。

除了数据映射之外，我们还需要通过 [`echarts.graphic`](https://echarts.apache.org/zh/api.html#echarts.graphic) 中的函数生成要渲染的图形，例如想渲染矩形则使用 [`echarts.graphic.clipRectByRect`](https://echarts.apache.org/zh/api.html#echarts.graphic.clipRectByRect)。

准备好上述内容之后，就可以设定 [`返回值`](https://echarts.apache.org/zh/option.html#series-custom.renderItem)了，可以返回 `rect` 、`line` 等。

### 关于数据映射的理解

自己写的时候对文档中描述的数据映射的概念特别模糊，但后面想想其实很简单，示例代码如下：

```javascript
renderItem(params, api) {
  var coord = api.coord([0, 1]);
  console.log(coord[0]) // x 轴上第一个刻度的坐标点的横坐标值
  console.log(coord[1]) // y 轴为第二个刻度的坐标点的纵坐标值
}
```

上述代码我将`[0, 1]` 作为参数传入 `api.coord` 中，分别得到 x 轴上第一个刻度的坐标点的横坐标值和 y 轴为第二个刻度的坐标点的纵坐标值。

### 需要留意的地方

- 把 `0` 作为参数传入 `api.coord` 和 `api.size` ，会返回 x 轴或 y 轴第一个刻度的数据信息，并不是原点。
- 把非整数作为参数传入 `api.coord` 和 `api.size` ，参数会先进行取整，再进行换算，例如，`0` 和 `0.5` 得到的结果是一样的。
- `api.value` 的参数不能超过 `3`，无论当前 data 的 value 数组的长度是否超过 `3` 。

## 案例

这边自己写了一个 [demo](https://trcat.github.io/echart/)，生成如下图表，看过源码之后会对上述内容有更好的理解：
![demo](demo.png)