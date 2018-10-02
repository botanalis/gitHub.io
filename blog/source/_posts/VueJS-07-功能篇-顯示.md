---
title: '[VueJS][07][功能篇]-顯示'
date: 2018-10-02 14:03:18
tags: VueJs
---

# 顯示判斷邏輯

使用`v-show`標籤語法，判斷資料顯示

## v-show語法
~~~html
<div v-show="Boolean">
</div>
~~~

> Boolean(布林值)：true(顯示) / false（隱藏）


<!--more-->

## 範例

顯示`<div>`標籤區塊

>下述顯示 **I'm a ghost! Boo!** 字串。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][07]show-1</title>
</head>
<body>
    <div id="app">
        <div v-show="isNight">
            I'm a ghost! Boo!
        </div>
        <div v-show="!isNight">
            I'm a Night! Boo!
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
       
        new Vue({
            el: '#app',
            data:{
                isNight: true
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 07_Example_1.png %}