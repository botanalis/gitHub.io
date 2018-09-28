---
title: '[VueJS][01][基礎篇]-語法'
date: 2018-09-28 16:03:42
tags: VueJs
---

# VueJS 簡介

{% asset_img 01_1_vuelog.png %}

輕量化 JavaScript MVC 前端框架，可以將前端網頁資料與Html元素大量的簡化，使網頁資料更佳的編寫與體驗。

詳細VueJS說明請參考官方網站：[https://vuejs.org](https://vuejs.org)

<!--more-->

## VueJs 基本語法

◉引用Vue JavaScript CND :

~~~javascript
https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js
~~~

---

◉VueJs語法：

~~~javascript
new Vue({
	el: '#app',
	data:{
		...
	}
});
~~~

> `el` : 指定作用區塊標籤id(#app)或class(.app)
> `data` : 資料Object

---

◉Html宣告：

~~~html
<body>
	<div id="app">
		{{title}}
	</div>
</body>
~~~

> `{ {   } }` : VueJs運算區塊

---

### 網頁Html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][01]簡介</title>
</head>
<body>
    <div id="app">
        <h2>{{title}}</h2>
        <ul>
            <li>{{items[0]}}</li>
            <li>{{items[1]}}</li>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        var myList = {
            title: 'My Shopping List',
            items: ['Bananas', 'Apples']
        };

        new Vue({
            el: '#app',
            data: myList
        });
    </script>
</body>
</html>
~~~

### 網頁結果

{% asset_img 01_Example_1.png %}