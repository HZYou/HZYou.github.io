---
layout:     post
title:      JavaScript 散记
subtitle:   记录 JavaScript 不易理解、散知识点等，不定期更新
date:       2019-09-25
author:     You
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - JavaScript
    - 技术
---

## Object 对象

### 原型及原型链
原型是一个对象，原型链是一串原型

### 对象属性

对象的属性可分为：
- 自有属性/继承属性

- 可枚举属性/不可枚举属性

#### 检查属性的方法

1. for/in  循环出自有属性和继承属性

2. hasOwnPreperty()/Object.getOwnPrepertyNames()

  - `hasOwnPreperty()` :检测属性是否是对象的自有属性，是返回true，否返回false

  - `Object.getOwnPrepertyNames()` :返回对象自有属性**名** 组成的数组

3. prepertyIsEnumerable()/Object.keys()

 - `prepertyIsEnumerable()` :属性是自有属性且是可枚举的属性，返回true;

 - ` Object.keys()` :返回对象的可枚举的自有属性的**名称**组成的数组

#### 存取器属性 getter/setter

####  对象定义存取器属性的方法：
```javascript
var obj ={
  get accessor_prop(){},
  set accessor_prop(value){}
}
```
#### 属性的特性

属性包含名字和4个特性；4个特性：值（value）、可写性（writalbe）、可枚举（enumerable）、可配置（configurable）; 

存取器属性的四个特性是：存、取、可枚举、可配置

属性描述符 `Object.getOwnPropertyDescriptor()`只能得到自有属性的描述符

设置属性的特性：

```javascript
Object.defineProperty(obj,prop,{value:1,writable:true,enumerable:false,configurable:ture});
```

设置多个属性的特性：
```javascript
Object.definePropertys(obj,{prop:{value:1},prop2:{value:2}})
```


#### 对象的三个属性

每个对象都有与之对应的：原型（prototype)、类（class）、可扩展性（extensible attribute)

**原型属性**
- 查询对象的原型属性：`Object.getPrototypeOf(obj);`
- 判断P是否是S的原型：`P.isPrototypeOf(S)`

**类属性**
是一个字符串，用以表示对象的类型信息。

**可扩展性**
用以表示是否可以给对象添加属性。

- `Object.isExtensible();` : 查询对象是否可扩展
- `Object.preventExtensions();` : 禁止扩展
- `Object.seal()` : 将对象设置：不可扩展且所有自有属性设置为不可配置，已有可写属性依旧可以设置
- `Object.isSealed()` ：检测对象是否封闭
- `Object.freeze()` : 冻结对象：不可扩展、不可配置，属性只读
- `Object.isFrozen()` : 检测对象是否冻结

#### 对象方法

`toString()`
`toLocaleString() ` 对数字、日期、时间做本地化转换
`toJSON()` : 转化成JSON字符串
`valueOf()` : 对象转换为原始值而非字符串时才会调用
`hasOwnProtery()`  ：检测对象是否含有特定的自身属性，该方法会忽略掉那些从原型链上继承到的属性
`propertyIsEnumerable()`  ：确定指定的属性是否可枚举，即被for...in循环枚举，但是通过原型链继承的属性除外
`prototypeObj.isPrototypeOf(object)` ： 搜寻prototypeObj否在参数object的原型链上


## 函数的5种调用模式

- 函数模式：this表示全局对象（浏览器中是window，在node 中是 global）
- 构造器 (constructor) 模式： this 表示刚刚创建出来的对象
- 方法（method）模式：this 表示引导方法调用的对象
- 上下文（context）模式：this 可以使用参数来动态的描述（动态绑定）
- bind 模式：this 与上下文模式类似，也是通过参数来确定（静态绑定）

### 上下文

函数在执行的时候会创建活动对象，活动对象中会存在一个上下文，就是函数中的this；
call 和 apply 方法的第一个参数就是决定上下文的东西
1. 传入什么 上下文 就是什么（this就是什么）
2. 传入引用类型，除 null 外this就是此引用类型
3. 传入基本类型，this 是它们转换成包装类型后的值
4. 传入 null、undefined，上下文就是全局对象

