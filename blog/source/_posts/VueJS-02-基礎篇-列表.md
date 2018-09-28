---
title: '[VueJS][02][基礎篇]-列表'
date: 2018-09-28 16:11:58
tags: VueJs
---

# 顯示資料清單

使用`v-for`標籤語法，顯示資料清單

## v-for 迴圈語法

~~~html
<div v-for=" x in 陣列Object" ></div>
<div v-for=" (object, index) in 陣列Object" ></div>
~~~

> x : 陣列取出的Object(class/int/string)值。

> (object, index) : index索引值。

> 陣列Object : 物件可以為class/int/string陣列。

<!--more-->

## 數字範圍

從10~1顯示結果

> 註記：起始值由 1 開始，非 0 開始。

### 網頁Html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][02]v-for</title>
</head>
<body>
    <div id="app">
        <ul>
            <li  v-for="n in 10">
              {{ 11 - n}}
            </li>
            <li>~End~</li>
          </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app'
        });
    </script>
</body>
</html>
~~~

### 網頁結果 

{% asset_img 02_Example_1.png %}

## 陣列

顯示陣列內容清單

### 網頁Html -【陣列資料放在html標籤】

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][02]v-for 陣列-1</title>
</head>
<body>
    <div id="app">
        <ul>
            <li  v-for="n in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]">
              {{ 11 - n}}
            </li>
            <li>~End~</li>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app'
        });
    </script>
</body>
</html>
~~~

### 網頁Html -【陣列資料放在VueJs Data屬性】

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][02]v-for 陣列-2</title>
</head>
<body>
    <div id="app">
        <ul>
            <li  v-for="n in countdoen">
              {{ 11 - n}}
            </li>
            <li>~End~</li>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data:{
                countdoen:[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果 

{% asset_img 02_Example_1.png %}

## 陣列【索引】

顯示陣列清單索引值內容

> 下述 `The { { animal } } goes { { sounds[i] } }` 中，透過 `i` 索引值來指定 `sounds`陣列字串。

### 網頁Html -【陣列資料放在html標籤】

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][02]v-for 陣列-3</title>
</head>
<body>
    <div id="app">
        <ul>
            <li  v-for="(animal, i) in animals">
              The {{ animal }} goes {{ sounds[i] }}
            </li>
          </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data:{
                animals:['dog', 'cat', 'bird'],
                sounds:['woof', 'meow', 'tweet']
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果 

{% asset_img 02_Example_2-3.png %}

## 物件陣列

顯示物件內容值

> 下述 `(sound, name) in animals`中，`sound`為 key 值，`name`為value值，
完整語法：

> v-for="(key, value) in Object"。

> v-for="(key, value, index) in Object"。

### 網頁Html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][02]v-for 物件陣列-1</title>
</head>
<body>
    <div id="app">
        <ul>
            <li  v-for="(sound, name) in animals">
              The {{ name }} goes {{ sound }}
            </li>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data:{
                animals:{
                    dog: 'woof', cat: 'meow', bird: 'tweet'
                }
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果 

{% asset_img 02_Example_3-1.png %}


## 物件陣列【索引】

顯示物件內容值

### 網頁Html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][02]v-for 物件陣列-2</title>
</head>
<body>
    <div id="app">
        <ul>
            <li  v-for="(sound, name, index) in animals">
              {{ index }} - The {{ name }} goes {{ sound }}
            </li>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data:{
                animals:{
                    dog: 'woof', cat: 'meow', bird: 'tweet'
                }
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果 

{% asset_img 02_Example_3-2.png %}