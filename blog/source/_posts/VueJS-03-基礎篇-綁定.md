---
title: '[VueJS][03][基礎篇]-綁定'
date: 2018-09-28 16:39:37
tags: VueJs
---

# 單向綁定資料

使用`v-model`標籤語法，將html元素與VueJs資料進行Match。

## v-model 語法

~~~html
<input v-model="DataName" />
~~~

> DataName: 根據VueJs data屬性欄位中宣告之名稱 

<!--more-->

## 範例

顯示輸入字串訊息

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][03]v-model 單向資料綁定-1</title>
</head>
<body>
    <div id="app">
        <input v-model="message" />
        <p>input[ {{message}} ] </p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data:{
                message: 'VueJs Model'
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 03_Example_1.gif%}