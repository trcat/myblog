---
title: CSS3 变量
date: 2021-06-08 20:18:06
copyright: true
abstract: 工作需要了解了一下CSS3变量内容，简单记录一下。
categories:
- [计算机技术]
tags:
- css
---

# CSS3 变量



## 在 SCSS 中使用

### 基本使用

```scss
$--font-size: 20px;

:root {
  --font-size: #{$--font-size};
}

.app {
  font-size: var(--font-size);
}
```

### bootstrap 中使用案例

通过 `@each` 遍历 list 变量并在 `:root` 中声明

```scss
$colors: (
  "blue":       $blue,
  "indigo":     $indigo,
  "purple":     $purple,
  "pink":       $pink,
  "red":        $red,
  "orange":     $orange,
  "yellow":     $yellow,
  "green":      $green,
  "teal":       $teal,
  "cyan":       $cyan,
  "white":      $white,
  "gray":       $gray-600,
  "gray-dark":  $gray-800
) !default;

:root {
  @each $color, $value in $colors {
    --#{$variable-prefix}#{$color}: #{$value};
  }
}
```

scss 文件中既有用到 scss 变量也有用到 css 变量定义样式，js 通过 `getPropertyValue` 获取变量的值

```scss
.navbar-nav-scroll {
  max-height: var(--#{$variable-prefix}scroll-height, 75vh);
  overflow-y: auto;
}
```

```js
const isEnd = getComputedStyle(this._menu).getPropertyValue('--bs-position').trim() === 'end';
```



> 个人猜测，使用时方便全局修改的用 css 变量赋值。

 ### ant design 中的使用

```less
html {
  --antd-wave-shadow-color: @primary-color;
  --scroll-bar: 0;
}
```

主要用在 less 文件中，在组件中时候是也存在通过 javascript 修改变量的情况

```jsx
    function renderCloseIcon() {
      return (
        closable && (
          <button
            type="button"
            onClick={onClose}
            aria-label="Close"
            className={`${prefixCls}-close`}
            style={
              {
                '--scroll-bar': `${getScrollBarSize()}px`,
              } as any
            }
          >
            {closeIcon}
          </button>
        )
      );
    }
```

### 优先级

css 变量的优先级规则和 selector 的一样

```scss
:root{
  --font-size: 12px;
}

body {
  --font-size: 20px;
  div {
    font-size: var(--font-size) // 20px
  }
}
```



### 目前发现的使用上的限制

在 scss 文件中使用 css 变量和在 css 文件中使用 css 变量是不一样的

#### 字符串的拼接

css 变量进行字符串拼接目前发现只能在 `content` 中使用。

```scss
// 源码
body {
  font-family: var(--font-family)" New"; // "Courier New"
  &:before {
    content: var(--css-prefix) "ed" // red
  }
}
// 编译后
body {
  font-family: var(--font-family) " New"; // 无效
}
body:before {
  content: var(--css-prefix) "ed"; // red
}
```



## 默认值

`var(<custom-property-name>, <declaration-value>)`  可以传入两个参数，第一个参数就是自定义属性值，第二个为回退值，当自定义属性值无效时使用回退值。

```css
.component .header {
  color: var(--header-color, blue); /* header-color isn’t set, and so remains blue, the fallback value */
  background-image:var(--bg-img, url(./one.png), url(./two.png));
}

// 结果为
.component .header {
  color: blue;
  background-image: url(./one.png), url(./two.png)
}
```



## 兼容性处理

```css

a {
  color: #7F583F;
  color: var(--primary);
}

```

```css

@supports ( (--a: 0)) {
  /* supported */
}

@supports ( not (--a: 0)) {
  /* not supported */
}

/* @supports IE 也不支持 */

```



## 参考文献

- https://juejin.cn/post/6844904084936327182
- http://www.ruanyifeng.com/blog/2017/05/css-variables.html



## 字体主题修改方案

在 `./src/index.scss` 文件夹中在 `:root` 上定义变量

```scss
// index.scss
:root {
  --font-size-small: #{$--theme-font-size-small};
  --font-size-default: #{$--theme-font-size-default};
  --font-size-large: #{$--theme-font-size-large};
}
```

使用时，还是要和之前一样，建立主题文档，并走 gulp 编译，这样`:root` 中的变量也会随之修改。

考虑到兼容性问题，能获取到 scss 变量的还是使用 scss 变量，否则则在项目中通过 `var()` 使用 css 变量：

```scss
selector {
  font-size: 14px; // 避免浏览器不支持
  font-size: var(--font-size, 14px); // 第二个参数防止没有设定变量
}
```

### 方案优化

- 考虑能否优化在 scss 中声明 css 变量的方式



