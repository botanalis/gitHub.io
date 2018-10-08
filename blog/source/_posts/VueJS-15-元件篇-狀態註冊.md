---
title: '[VueJS][15][元件篇]-狀態註冊'
date: 2018-10-09 00:33:38
tags: VueJs
---

# 狀態註冊

使用Html標籤`ref`，將自己的狀態註冊到root，提供全域變數存取。

<!--more-->

## 語法

~~~html
<templement ref="refName"></templement>
~~~

>使用ref標籤進行註冊，透過$refs.refName.parament來存取變數。

## 範例(一)

狀態註冊

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][15]status-1</title>
</head>
<body>
    <div id="app">
        <child ref="junior"></child>
        <p>Trunth: {{childStomach}}</p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'child',
            {
                template: "<p>{{mouth}}</p>",
                data(){
                    return {
                        mouth: 'I didn`t eat that cookie',
                        stomach: 'Yummy that cookie was delicious.'
                    }
                }
        });

        new Vue({
            el:'#app',
            data:{
                childStomach: 'unknown'
            },
            mounted(){
                this.childStomach = this.$refs.junior.stomach
            }
        });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 15_Example_1.png %}

## 範例(二)

狀態註冊

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][15]status-2</title>
</head>
<body>
    <div id="app">
        <child v-for="i in 10" ref="junior" :num="i" :key="i"></child>
        <p>Trunth for child 4: {{child4Stomach}}</p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'child',
            {
                template: "<p>{{num}}: {{mouth}}</p>",
                props: ['num'],
                data(){
                    return {
                        mouth: 'I didn`t eat that cookie',
                        stomach: 'Yummy that cookie was '+ this.num+ ' times more delicious.'
                    }
                }
        });

        new Vue({
            el:'#app',
            data:{
                child4Stomach: 'unknown'
            },
            mounted(){
                this.child4Stomach = this.$refs.junior[3].stomach
            }
        });

    </script>
</body>
</html>

~~~

### 網頁結果
{% asset_img 15_Example_2.png %}
