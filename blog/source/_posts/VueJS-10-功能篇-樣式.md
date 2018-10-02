---
title: '[VueJS][10][功能篇]-樣式'
date: 2018-10-02 17:59:33
tags: VueJs
---

# Style CSS 變更

使用`v-bind`標籤語法，綁定class、style。

## v-bind語法
~~~html
<div v-bind:class=" [樣式/宣告data名稱] : [Boolean(true/false)] ">
</div>

<div :class=" [樣式/宣告data名稱] : [Boolean(true/false)] ">
</div>
~~~

多個樣式

~~~html
<div v-bind:class=" [樣式/宣告data名稱] : [Boolean(true/false)] , [樣式/宣告data名稱] : [Boolean(true/false)] , ... ">
</div>
~~~

> (1).語法糖： **`v-bind:class`** 可以簡寫為 **`:class`** 。
> 
> (2).v-bind:class="{ 樣式/宣告data名稱 : bool(true/false)}" : 表示`true`使用該樣式。

<!--more-->

## 範例(一)

TextArea輸入字串數量達到40個字以上時，將輸入方塊底色改成粉紅色提示。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][10]style-1</title>
</head>
<body>
    <div id="app">
        <textarea v-model="memeText" 
            :class="{ warn: longText}"
            :maxlength="limit">
        </textarea>
        <p>{{memeText.length}}</p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
       
       new Vue({
            el: '#app',
            data:{
                memeText: 'What if I told you CSS can do that',
                limit: 50
            },
            computed:{
                longText(){
                    if(this.limit - this.memeText.length <= 10){
                        return true;
                    }else{
                        return false;
                    }
                }
            }
        });

    </script>
</body>
</html>


<style>
.warn{
  background-color: mistyrose;
}
</style>
~~~

### 網頁結果
{% asset_img 10_Example_1.gif %}

## 範例(二)-模組化

TextArea輸入字串數量達到40個字以上時，將輸入方塊底色改成粉紅色提示。

>將判斷字串長度處理邏輯移到Method。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][10]style-2</title>
</head>
<body>
    <div id="app">
        <textarea v-model="memeText" 
            :class="classes">
        </textarea>
        <p>{{memeText.length}}
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                memeText: 'What if I told you CSS can do that',
                limit: 50
            },
            methods:{
                longText(textlong){
                    if(textlong <= 10){
                        return true;
                    }else{
                        return false;
                    }
                }
            },
            computed:{
                classes(){
                    return { warn : this.longText(this.limit - this.memeText.length) } ;
                }
            }
        });

    </script>
</body>
</html>


<style>
.warn{
  background-color: mistyrose;
}
</style>
~~~

### 網頁結果
{% asset_img 10_Example_2.gif %}
