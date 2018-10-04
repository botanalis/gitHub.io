---
title: '[VueJS][12][功能篇]-動畫'
date: 2018-10-03 16:26:57
tags: VueJs
---

# 轉場渲染

{% asset_img 12_Content_1.png %}

<!--more-->

## VueJs動畫分為進場/離場階段

### 進場三階段

1. v-enter：進入前。

2. v-enter-active：進入執行中。

3. v-enter-enter-to：進入結束。

### 離場三階段

1. v-leave：離開前。

2. v-leave-active：離開執行中。

3. v-leave-to：離開結束。

## VueJs提供自訂宣告
自行定義可以搭配使用三方套件`Animate.css`或是`自行定義css樣式`。

### 自訂宣告進場三階段

1. enter-class：進入前。

2. enter-active-class：進入執行中。

3. enter-to-class：進入結束。


### 自訂宣告離場三階段

1. leave-class：離開前。

2. leave-active-class：離開執行中。

3. leave-to-class：離開結束。

## 語法
~~~html
<transition name="myTransition"></transition>
~~~

> myTransition: 動畫名稱。

-
> 當指定名稱時，VueJs就會自動將class轉換成如下【根據下述lass名稱定義css樣式】：
> 
> myTransition-enter-class：進入前。
> 
> myTransition-enter-active-class：進入執行中。
> 
> myTransition-enter-enter-to-class：進入結束。
> 
> myTransition-leave-class：離開前。
> 
> myTransition-leave-active-class：離開執行中。
> 
> myTransition-leave-to-class：離開結束。



## 範例(一)

會動的車子

> 使用第三方套件[Animate.css](https://daneden.github.io/animate.css/)

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-1</title>
</head>
<body>
    <div id="app">
        <button @click="taxiCalled=true">Call a cab</button>
        <transition enter-active-class="animated slideInRight">
            <p v-if="taxiCalled">🚕</p>
        </transition>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                taxiCalled: false
            }
        });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 12_Example_1.gif%}

## 範例(二)

會動的車子(自定義CSS樣式)

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-2</title>
</head>
<body>
    <div id="app">
        <button @click="taxiCalled=true">Call a cab</button>
        <transition 
            enter-class="slideInRight"
            enter-active-class="go">
            <p v-if="taxiCalled">🚕</p>
        </transition>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                taxiCalled: false
            }
        });

    </script>
</body>
</html>

<style>
.slideInRight{
  transform: translateX(200px);
}
.go{
  transition: all 2s ease-out;
}
</style>
~~~

### 網頁結果
{% asset_img 12_Example_2.gif%}

## 範例(三)

載入圖片

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-3</title>
</head>
<body>
    <h1>The Fill Murray Page</h1>
    <div id="app">
        <transition appear>
            <img src="https://fillmurray.com/50/70" width="50" height="70">
        </transition>
        <p>
            The internet was missing the ability to 
            provide custom-sized placeholder images of Bill Murray.
            Now it can.
        </p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app'
        });

    </script>
</body>
</html>

<style>
img{
  float: left;
  padding: 5px;
}
.v-enter{
  opacity: 0;
}
.v-enter-active{
  transition: opacity 2s;
}

</style>
~~~

### 網頁結果
{% asset_img 12_Example_3.gif%}

## 範例(四)

變換顯示(按三次Kiss button青蛙變公主)

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-4</title>
</head>
<body>
    <div id="app">
        <button @click="kisses++">💋Kiss!</button>
        <transition name="fade">
            <p v-if="kisses < 3 " key="frog">🐸frog</p>
            <p v-if="kisses >= 3" key="princess">👸princess</p>
        </transition>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                kisses: 0
            }
        });

    </script>
</body>
</html>

<style>
.fade-enter-active, .fade-leave-active{
  transition: opacity .5s;
}

.fade-enter, .fade-leave-active{
  opacity: 0;
}
p{
  margin: 0;
  position: absolute;
  font-size: 3em;
}

</style>
~~~

### 網頁結果
{% asset_img 12_Example_4.gif%}

## 範例(五)

多變換顯示(隱藏人物出現)

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-5</title>
</head>
<body>
    <div id="app">
        <button @click="kisses++">💋Kiss!</button>
        <transition name="fade">
            <p v-if="kisses < 3 " key="frog">🐸frog</p>
            <p v-if="kisses >= 3 && kisses <= 5" key="princess">👸princess</p>
            <p v-else key="santa">🎅santa</p>
        </transition>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                kisses: 0
            }
        });

    </script>
</body>
</html>

<style>
.fade-enter-active, .fade-leave-active{
  transition: opacity .5s;
}
.fade-enter, .fade-leave-active{
  opacity: 0;
}
p{
  margin: 0;
  position: absolute;
  font-size: 3em;
}
</style>
~~~

### 網頁結果
{% asset_img 12_Example_5.gif%}

## 範例(六)

切換顯示

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-6</title>
</head>
<body>
    <div id="app">
        <button @click="product++">next</button>
        <transition name="slide">
            <p :key="products[product % 4]">{{products[product % 4]}}</p>
        </transition>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                product: 0,
                products:['☂️umbrella', '🖥computer', '🏀ball', '📷camera']
            }
        });

    </script>
</body>
</html>

<style>
.slide-enter-active, .slide-leave-active{
  transition: fransform .5s;
}
.slide-enter{
  transform: translateX(300px);
}
.slide-leave-active{
  transform: translateX(-300px);
}
p{
  margin: 0;
  font-size: 3em;
}
</style>
~~~

### 網頁結果
{% asset_img 12_Example_6.gif%}

## 範例(七)

刪除項目渲染

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-7</title>
</head>
<body>
    <div id="app">
        <h3>Syllabus</h3>
        <ul>
            <transition-group tag="ul">
                <li v-for="topic in syllabus" :key="topic">
                    <button @click="completed(topic)">Done</button>{{topic}}
                </li>
            </transition-group>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                syllabus:['HTML', 'CSS', 'Scratch', 'JavaScript', 'Python']
            },
            methods:{
                completed(topic){
                    let index = this.syllabus.indexOf(topic);
                    this.syllabus.splice(index, 1);
                }
            }
        });

    </script>
</body>
</html>

<style>
.v-leave-active {
  transition: all 1s;
  opacity: 0;
  transform: translateY(-30px);
}
</style>
~~~

### 網頁結果
{% asset_img 12_Example_7.gif%}

## 範例(八)

動畫

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css">
    <title>[VueJS][12]transition-8</title>
</head>
<body>
    <div id="app">
        <h3>Bus station simulator</h3>
        <transition-group tag="p" name="station">
            <spen v-for="bus in buses" :key="bus">🚌</spen>    
        </transition-group>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data: {
                buses: [1, 2, 3, 4, 5],
                nextBus: 6
            },
            mounted() {
                setInterval(() => {
                    const headOrTail = () => Math.random() >= 0.5;
                    if (headOrTail()) {
                        this.buses.push(this.nextBus);
                        this.nextBus += 1;
                    } else {
                        this.buses.splice(0, 1);
                    }
                }, 2000);
            }
        });

    </script>
</body>
</html>

<style>
.station-leave-active, .station-enter-active{
  transition: all 2s;
  position: absolute;
}
.station-leave-active {
  opacity: 0;
  position: absolute;
  transform: translateX(-30px);
}
.station-enter{
  opacity: 0;
  transform: translateX(30px); 
}
span{
  display: inline-block;
  margin: 3px;
}
</style>
~~~

### 網頁結果
{% asset_img 12_Example_8.gif%}