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

## 範例(一)

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

## 範例(二)
將資料進行轉換顯示出結果

> 使用 [accounting.js](https://github.com/openexchangerates/accounting.js) 套件，進行資料格式轉換 。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][05]filter-2</title>
</head>
<body>
    <div id="app">
        I have {{ 5 | currency }} in my pocket
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/accounting.js/0.4.1/accounting.js"></script>

    <script>
        
        Vue.filter('currency', function(money){
            return accounting.formatMoney(money);
        });

        new Vue({
            el: '#app'
        });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 05_Example_2.png%}

## 範例(三)
清單欄位格式顯示

> 使用 [accounting.js](https://github.com/openexchangerates/accounting.js) 套件，進行資料格式轉換 。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][05]filter-3</title>
</head>
<body>
    <div id="app">
        <table border="1">
            <thead>
                <tr>
                    <th>Item</th>
                    <th>Price</th>
                </tr>
            </thead>
            <thody>
                <tr v-for="item in inventory">
                    <td>{{item.name}}</td>
                    <td class="price">{{item.price | dollars}}</td>
                </tr>
            </thody>
        </table>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/accounting.js/0.4.1/accounting.js"></script>

    <script>
        
        Vue.filter('dollars', function(money){
            return accounting.formatMoney(money);
        });

        new Vue({
            el: '#app',
            data:{
                inventory:[
                    {
                        name: 'tape measure', 
                        price: '7'
                    },
                    {
                        name: 'stamp', 
                        price: '0.01'
                    },
                    {
                        name: 'shark tooth', 
                        price: '1.5'
                    },
                    {
                        name: 'iphone', 
                        price: '999'
                    }
                ]
            }
        });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 05_Example_3.png%}
