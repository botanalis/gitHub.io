---
title: '[VueJS][05][基礎篇]-過濾'
date: 2018-09-28 18:07:50
tags: VueJs
---

# 通道預先處理

使用`Vue.filter()`宣告處理Method。

## filter語法
~~~html
Vue.filter('filterName', function(){
 ...
});
~~~

> filterName: 過濾器名稱。
>
> function(){} : Mehtod處理邏輯實作。

<!--more-->

## 範例

將字串自首轉成大寫

>下述 **{{ message  | capitalize }}** ，使用「 ｜ 」符號呼叫使用Filter。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][05]filter-1</title>
</head>
<body>
    <div id="app">
        <input v-model="message" />
        <p>Original[ {{message}} ] </p>
        <p>Filter[ {{message  | capitalize }} ]</p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        
        Vue.filter('capitalize', function(string){
            var capitalFirst = string.charAt(0).toUpperCase();
            var noCaseTail = string.slice(1, string.length);
            return capitalFirst + noCaseTail;
        });
        
        
        //===~ES6語法~===//
        /*
        Vue.filter('capitalize', function(string){
            var  [first, ...tail] = string;
            return first.toUpperCase() + tail.join('');
        });
        */

        new Vue({
            el: '#app',
            data:{
                message: 'hello world'
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 05_Example_1.gif%}