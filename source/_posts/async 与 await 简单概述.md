---
title: async 与 await 简单概述
date: 2018-06-01 11:23:23
tags: 
categories: [es7]
---


async/await 是什么？

async 函数是 Generator 函数的语法糖。使用 关键字 async 来表示，在函数内部使用 await 来表示异步。

async 表示这是一个 async 函数，而 await 只能在这个函数里面使用。

await 表示在这里等待 await 后面的操作执行完毕，再执行下一句代码。

await 后面紧跟着的最好是一个耗时的操作或者是一个异步操作。


#### 基本用法
async函数返回一个 Promise对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。
下面是一个例子，指定多少毫秒后输出一个值：
```javascript
function timeout(time) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve();
        },time)
    })
}
async function print(value, time){
    await timeout(time);
    console.log(value);
}
print('hello world', 3000)
```
上面代码指定3秒以后，输出hello world。


#### 语法
async函数返回一个 Promise 对象。
async函数内部return语句返回的值，会成为then方法回调函数的参数。
```javascript
async function f() {
  return 'hello world';
}

f().then(v => console.log(v))
```

#### 并行
将多个promise直接发起请求（先执行async所在函数），然后再进行await操作。
```javascript
async function asyncAwaitFn(str) {
    return await new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(str)
        }, 1000);
    })
}
const test = async () => { //并行执行
    const testOne = asyncAwaitFn('string 1');
    const testTwo = asyncAwaitFn('string 2')
    console.log(await testOne)
    console.log(await testTwo)
}
test()
```
把多个串行请求改为并行可以将代码执行得更快，效率更高。