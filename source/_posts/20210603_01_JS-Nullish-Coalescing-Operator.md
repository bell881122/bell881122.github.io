---
title: 【JS】雙問號 ?? 運算子
date: '2021-06-03 00:00:01'
tags: [JavaScript]
cover: https://cdn.pixabay.com/photo/2017/07/10/23/43/question-mark-2492009_960_720.jpg
---

![【JS】雙問號 ?? 運算子](https://cdn.pixabay.com/photo/2017/07/10/23/43/question-mark-2492009_960_720.jpg)

# ?? 運算子
全名 Nullish Coalescing Operator
是 null 與 undefined 專用運算子

## 作用
當前項的值為 null 或 undefined 時
帶入後項的預設值

## 使用方法：
`Value ?? DefaultValue;`

## 使用實例：
```JavaScript
let number;

console.log(number ?? 10);
// 10

number = null;
console.log(number ?? 20);
// 20

number = 10;
console.log(number ?? 20);
// 10
```

<br/>
<hr>

# 參考資料
[Nullish coalescing operator (??)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)
[JavaScript 之旅 (25)：Nullish Coalescing Operator ( ?? 運算子)](https://ithelp.ithome.com.tw/articles/10251710)
<br/>