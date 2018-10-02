---
title: '[VueJS][09][功能篇]-內嵌'
date: 2018-10-02 16:23:37
tags: VueJs
---

# 簡易Html樣板

使用`v-html`標籤語法，替換區塊Html。

## v-if語法
~~~html
<div v-html="Html Template">
</div>
~~~

> Html Template：可以在 Vue data 屬性宣告Html。

<!--more-->

## 範例

顯示簡易Html Template。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][09]html-1</title>
</head>
<body>
    <div id="app">
        <div v-for="htmlT in htmlText">
            <div v-html="htmlT"></div>
            <hr>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
       
        new Vue({
            el: '#app',
            data:{
                htmlText:[
                    'Dear John,<br/>thank you for the <pre>Batman vs Auperman</pre>DVD!',
                    'Dear John,<br/>thank you for <i>Ghostbusters 3</i> !',
                    'Dear John,<br/>thanks, <b>Gods of Egypt</b> is my new favourite!'
                ]
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 09_Example_1.png %}