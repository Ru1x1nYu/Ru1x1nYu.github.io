---
title: React Hooks指南（1） useState
date: 2020-09-01 14:02:56
tags:
---
## 前言 ##
在class内部，Hook不起作用。
### 规则 ###
1. 在函数组件中，Hook只能在函数最顶层使用，切勿在循环、条件或嵌套函数中调用Hook，以确保React能按Hook调用的顺序运行；
2. 不要在普通的js函数中调用hook，hook只能在函数组件或者自定义hook中调用。
> eslint插件： eslint-plugin-react-hooks
使用该插件能够强制开发者遵守执行这两条规则。

`npm install eslint-plugin-react-hooks --save-dev`
``` 
// 你的 ESLint 配置
{
  "plugins": [
    // ...
    "react-hooks"
  ],
  "rules": {
    // ...
    "react-hooks/rules-of-hooks": "error", // 检查 Hook 的规则
    "react-hooks/exhaustive-deps": "warn" // 检查 effect 的依赖
  }
}
```
## 介绍 ##
+ React函数组件没有实例，也没有状态，class组件可以使用this.   state.[data]去操作函数状态函数组件的状态需要使用useState钩子去声明定义。

## 使用 ##
在react文件中引入：
> import React, { useState } from 'react';

在函数顶部调用useState，传入参数为当前状态的初始值，可以不传，默认空值。useState方法返回两个值，第一个是当前声明状态的属性，第二个是修改该状态的方法。

`const [name, setName] = useState('aYu')`
## 原理 ##
```
let memoizedStates = [] // 多个useState
let index = 0
function useState (initial) {
    memoizedStates[index] = memoizedStates[index] || initial
    let currentIndex = index
    function setState(newState) {
        memoizedStates[currentIndex] = newState
        render()
    }
    return [memoizedStates[index++], setState]
}
```