---
title: '[VueJS][04][基礎篇]-事件'
date: 2018-09-28 17:30:28
tags: VueJs
---

# 事件綁定

使用`v-on`標籤語法，將html元素與VueJs Methods進行Match。

## v-on語法
~~~html
<button v-on:click="MethodName"></button>
~~~

> MethodName: 根據VueJs methods屬性中宣告之名稱。

<!--more-->

## 範例

點擊Button遞增數值

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][04]v-on 事件綁定-1</title>
</head>
<body>
    <div id="app">
        <button v-on:click="toast">Toast bread</button>
        <input v-model="toastedBreads" />
        <p>Quantity to put in the oven: {{toastedBreads}}</p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data:{
                toastedBreads: 0
            },
            methods:{
                toast() { 
                    this.toastedBreads++
                }
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 04_Example_1.gif%}