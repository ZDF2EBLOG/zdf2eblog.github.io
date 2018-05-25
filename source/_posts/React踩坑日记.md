---
title: React踩坑日记
date: 2018-05-25 15:19:35
tags: Jszy
categories: [React]
---

React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设Instagram 的网站。做出来以后，发现这套东西很好用，就在2013年5月开源了。(反正百度百科是这么说的~)

> 初略看了一下文档教程，就这么开始了React之旅。。。

### JSX语法

JSX算是React的核心部分啦，它的作用就是让你可以在js中书写XML，具有非常好的扩展性，特点如下：

- XML语法容易接受，结构清晰
- 增强JS语义
- 抽象程度高，屏蔽DOM操作，跨平台
- 代码模块化

```javascript
import React from 'react'
class Example extends React.Component() {
    state = {
        msg: 'This is a msg'
    }
    render() {
        const _msg = this.state.msg;
        return (
            <div className="container">
                {/* 注释是这样的 必须有顶层元素包裹 */}
                <h1>Hello World!!!</h1>
                <p>Welcome to React.</p>
                {/* 插入变量值 */}
                <div>{_msg}</div>

                {/* 添加样式 */}
                <div style={{backgroundColor: 'red'}}>这是个红色区域</div>
            </div>
        )
    }
}
```

### 组件的生命周期

React根据真实DOM的状态（渲染前/正在渲染/渲染后），提供相关处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用。

```
componentWillMount()
componentDidMount()
componentWillUpdate(object nextProps, object nextState)
componentDidUpdate(object prevProps, object prevState)
componentWillUnmount()
```

不仅如此，React还给我们提供了两种处理特殊状态的函数：

```javascript
// 已加载组件收到新的参数时调用
componentWillReceiveProps(object nextProps)
// 组件判断是否重新渲染时调用
shouldComponentUpdate(object nextProps, object nextState)
```

### 绑定点击事件

```javascript
import React from 'react'
class Example extends React.Component() {
    state = {
        isShow: true
    }
    handleClick() {
        this.setState({
            isShow: !isShow
        })
    }
    render() {
        return (
            /**
             * 绑定click事件
             * 点击按钮，实现内容切换
             */
            <div className="container">
                <button onClick={this.handleClick.bind(this)}>点击按钮</button>
                {this.state.isShow ? <div>
                    <h1>Title</h1>
                    <div>Content</div>
                </div> : ''}
            </div>
        )
    }
}
```

### 小技巧

渲染数组

```javascript
render() {
    const testArray = [1,2,3];
    return (
        <div className="container">
            <ul>
                {testArray.map((item, index) => {
                    <li key={index}>{item}</li>
                })}
            </ul>
        </div>
    )
}
```

封装基础类组件

比如 `<input type="text" >` 每次写很麻烦吧，可以封装一个成一个组件

```javascript
const input = (props) => {
    return <input type = {props.type} {...props} />
}
```

给setState传入function可以使用function来更新state

```javascript
this.setState((prevState, props) => {
    return ...
})
```
