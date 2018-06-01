---
title: Scss的简单使用
date: 2018-06-01 09:36:46
tags: Jszy
categories: [CSS]
---

Scss 是 Sass 3 引入新的语法，其语法完全兼容 CSS3，并且继承了 Sass 的强大功能。也就是说，任何标准的 CSS3 样式表都是具有相同语义的有效的 SCSS 文件。另外，SCSS 还能识别大部分 CSS hacks（一些 CSS 小技巧）和特定于浏览器的语法。

> 完全兼容 CSS3
> 在 CSS 基础上增加变量、嵌套 (nesting)、混合 (mixins) 等功能
> 通过函数进行颜色值与属性值的运算
> 提供控制指令 (control directives)等高级功能
> 自定义输出格式


### 选择嵌套

> 优点： 避免了重复输入父选择器，提高开发效率。

```
.box {
  color: #333;
  .title {
    font-size: 14px;
    p {
      color: #666;
    }
  }
}

// 编译为css
.box {
  color: #333;
}
.box .title {
  font-size: 14px;
}
.box .title p {
  color: #666;
}
```

### 父级选择 &

```
a {
  font-weight: bold;
  text-decoration: none;
  &:hove {
    text-decoration: underline;
  }
  &.active {
    color: red;
  }
}

// 编译为css
a {
  font-weight: bold;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
a.active {
  color: red;
}
```

### 属性嵌套

```
.box {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}

// 编译为css
.box {
  font-family: fantasy;
  font-size: 30em;
  font-weight: bold;
}

```

### 变量 $

> 变量以美元符号开头，赋值方法与 CSS 属性的写法一样

```
$width: 200px;
$blue: blue;

// 定义不可以重复赋值的变量
$test: #333 !default;
```


直接调用即可

```
.box {
  width: $width;
  background-color: $blue;
}
```

变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量），不在嵌套规则内定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加 !global 声明：

```
// 定义全局变量
$width: 200px !global;
```

### 插值语句 #{}

> 通过 #{} 插值语句可以在选择器或属性名中使用变量

```
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}

// 编译为css
p.foo {
  border-color: blue;
}
```

### 常见指令 `@import` `@extend` `@root`

#### `@import`

通常，@import 寻找 Sass 文件并将其导入，但在以下情况下，@import 仅作为普通的 CSS 语句，不会导入任何 Sass 文件。

- 文件拓展名是 .css；
- 文件名以 http:// 开头；
- 文件名是 url()；
- `@import` 包含 media queries。

```
@import 'foo.scss';
```

然后，@import同样可以嵌套使用：

假设a.scss文件有以下内容：

```
.test {
  color: blue;
}
```

在b.scss文件中使用：

```
.box {
  @import 'a.scss';
}

// 编译为css
.box .test {
  color: blue;
}
```

#### `@extend`

> 使用公共样式, 继承效果。

```
.btn {
  border: 1px solid #333;
  border: 5px;
  padding: 6px 8px;
}

.operate-btn {
  background-color: #red;
  @extend .btn;
}
```

#### `@root`

> 让某个选择器跳出根元素

```
.a {
  color: red;
  .b {
    color: blue;
    .c {
      @at-root & {
        color: green;
      }
    } 
  }
}

// 编译为css
.a {
  color: red;
}
.a .b {
  color: blue;
}
.c {
  color: green;
}
```

