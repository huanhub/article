---
title: assign、extend 和 merge的区别
date: 2017-08-02 10:31:07
tags:
  - 'javascript'
---

最近在coding 的时候经常看到 `lodash.assign`, `Object.assign`, `lodash.extend`,
`lodash.merge`、`$.extend`、 `$.merge` 这些函数， 这些函数名的字面意思看起来都很相似，好
像都是合并对象，但究竟有什么区别呢？

<!-- more -->

## lodash.assign
lodash.assign(object, [sources]), 官网定义的意思是说 将源对象可枚举的键为字符串属性合并
到目标对象，源对象会从左到右应用，后面的源对象会覆盖前面的源对象相同属性。

## Object.assign
Object.assign(target, ...sources)方法用于将所有可枚举的属性的值从一个或多个源对象复制到目标对象。
它将返回目标对象。

## lodash.extend
lodash.extend(object, [sources]) 这个方法类似于lodash.assign，它将源对象的自身和继承的可枚举的键为字符串属性合并到目标对象

## lodash.merge
lodash.merge(object, [sources]) 个方法类似于lodash.assign，它除了将源对象的自身和继承的可枚举字符串键控属性递归合并到目标对象中。如果存在目标属性为undefind，则会跳过该属性。数组和简单对象属性被递归合并。其他对象和值类型被赋值覆盖。源对象从左到右应用。后面的源对象会覆盖前面的源对象相同属性。

## $.extend
jQuery.extend([deep], target, object1, [objectN]) 用一个或多个其他对象来扩展一个对象，返回被扩展的对象。如果第一个参数设置为true，则jQuery返回一个深层次的副本，递归地复制找到的任何对象。否则的话，副本会与原对象共享结构。 未定义的属性将不会被复制，然而从对象的原型继承的属性将会被复制。

## $.merge
jQuery.merge(first, second), 合并两个数组

解释了这么多，还不如直接上代码

```js
  var o1 = {0: 1, a: 1, b: 2};
  var o2 = {a: {c: 1, d: 2}, b: 3};
  var o3 = {a: {c: 2, e: 1}}
  function Test() {
    this.tc = 1;
  }
  Test.prototype.td = 2;

  console.log(Object.assign({}, o1, o2))
  // {0: 1, a: {c: 1, d: 2,}, b: 3}
  console.log(o1)
  // {0: 1, a: 1, b: 2}

  // 如果没有指定一个空对象会修改到目标对象本身
  // console.log(Object.assign(o1, o2))
  // {0: 1, a: {c: 1, d: 2,}, b: 3}
  // console.log(o1)
  // {0: 1, a: {c: 1, d: 2,}, b: 3}

  console.log(Object.assign({}, o1, o2, o3))
  // {0: 1, a: {c: 2, e: 1,}, b: 3}

  // 不会合并原型上的属性  td 属性没有被合并上
  console.log(Object.assign({}, o1, o2, o3, new Test()))
  // {0: 1, a: {c: 2, e: 1,}, b: 3, tc: 1}
  console.log(lodash.assign({}, o1, o2, o3, new Test()))
  // {0: 1, a: {c: 2, e: 1,}, b: 3, tc: 1}

  console.log(lodash.extend({}, o1, o2, o3, new Test()))
  // {0: 1, a: {c: 2, e: 1,}, b: 3, tc: 1, td: 2}
  console.log($.extend({}, o1, o2, o3, new Test()))
  // {0: 1, a: {c: 2, e: 1,}, b: 3, tc: 1, td: 2}

  console.log(lodash.merge({}, o1, o2, o3, new Test()))
  // {0: 1, a: {c: 2, d: 2, e: 1,}, b: 3, tc: 1, td: 2}
  console.log($.extend(true, {}, o1, o2, o3, new Test()))
  // {0: 1, a: {c: 2, d: 2, e: 1,}, b: 3, tc: 1, td: 2}

```

## 总结

* `Object.assign` 和 `lodash.assign` 基本上是一样的，lodash 官网标注了 `lodash.assign`是
基于 `Object.assign` 的, 并且不会合并原型上的属性
* `lodash.extend` 和 `$.extend` 没有deep 参数的作用是一样的，都是浅复制，会把后面源对象属性
直接覆盖前面源对象的属性

* `lodash.merge` 和 `$.extend` deep参数为true 的作用是一样的，都是深复制，会把后面源对象的对象属性
和前面源对象的对象属性进行合并

* lodash 3.x 版本中 `extend` 和 `assign` 一样, 4.x 版本中会合并原型链上的属性

* lodash 4.x `extend` 是 `assignIn` 的别名
