---
title: '[VueJS][13][元件篇]-Component'
date: 2018-10-05 16:32:55
tags: VueJs
---

# 模組化

使用`Vue.component`語法，建立Html Template。

## Vue.component語法
~~~html
Vue.component( 'Name', {
    template: `Html Template`,
    props:['...'],
    data(){
       return {
           資料1: xxx 
           ...
       }
    }
});
~~~

> Name: Component元素名稱。
> 
> Html Template: 網頁元素樣板。
> 
> props: 參數宣告陣列(單向綁定)。
> 
> data: 資料宣告（ **注意：component的資料宣告是return function** ）


<!--more-->

## 範例(一)

簡易範例。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-1</title>
</head>
<body>
    <div id="app">
        <light-bulb></light-bulb>
        <light-bulb></light-bulb>
        <light-bulb></light-bulb>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'light-bulb',
            {
                template:
                            `
                                <div class='light-bulb'>
                                <p>💡Eureka!</p>
                                </div>
                            `
            }
        );

        new Vue({
            el: '#app'
        });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 13_Example_1.png %}

## 範例(二)

帶參數Component。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-2</title>
</head>
<body>
    <div id="app">
        <label>Sound level</label>
        <input type="number" v-model:number="soundLevel">
        <sounnd-icon :level="soundLevel"></sounnd-icon>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'sounnd-icon',
            {
                template: "<span>{{soundEmojis[level]}}</span>",
                props: ['level'],
                data(){
                    return {
                        soundEmojis: ['🔇', '🔈', '🔉', '🔊']
                    }
                }
            }
        );

    new Vue({
        el:'#app',
        data:{
            soundLevel: 0
        }
    });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 13_Example_2.gif %}

## 範例(三)

每2秒變化字串。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-3</title>
</head>
<body>
    <div id="app">
        <blabber></blabber>
        <blabber></blabber>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        var line = 0;
        Vue.component(
            'blabber',
            {
                template: "<p>{{dialogue[currentLine]}}</p>",
                data(){
                    return {
                        currentLine: 0,
                        dialogue:[
                            'hello',
                            'how are you?',
                            'fine thanks',
                            'let`s go drink!',
                            'alright, where?',
                            'to hello`s bar',
                            'hello?'
                        ]
                    }
                },
                mounted(){
                    setInterval(() => {
                        this.currentLine = line % this.dialogue.length;
                        line = line + 1;
                    }, 2000)
                }
            }
        );
        
        new Vue({
            el:'#app'
        });


    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 13_Example_3.gif %}

## 範例(四)

宣告object來控制字串。

>透過**bus object**來判斷，因二個blabber互相發出`$emit(‘line’)`事件，造成Vue Create時所建立的`$on(line)`事件，被二個blabber互相觸發，而內部`this.currentLine`因為被二個blabber相互更換，所以導致字串輪流變化。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-4</title>
</head>
<body>
    <div id="app">
        <blabber :ice-breaker="true"></blabber>
        <blabber></blabber>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        var bus = new Vue();
        Vue.component(
            'blabber',
            {
                template: "<p>{{dialogue[currentLine]}}</p>",
                data(){
                    return {
                        currentLine: this.iceBreaker ? 0 : -1,
                        dialogue:[
                        'hello',
                        'how are you?',
                        'fine thanks',
                        'let`s go drink!',
                        'alright, where?',
                        'to hello`s bar',
                        'hello?'
                        ],
                        iceBreaker:{
                            type: Boolean,
                            default: false
                        }
                    }
                },
                created () {
                    bus.$on('line', line => {
                        if (line !== this.currentLine) {
                            setTimeout(() => {
                                this.currentLine = (line + 1) % this.dialogue.length;
                                bus.$emit('line', this.currentLine);
                            }, 2000)
                        }
                    })
                },
                mounted () {
                    if (this.iceBreaker) {
                        bus.$emit('line', 0);
                    }
                }
            }
        );

        new Vue({
            el:'#app'
        });


    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 13_Example_4.gif %}

## 範例(五)

使用component中的mixins屬性。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-5</title>
</head>
<body>
    <div id="app">
        <man></man>
        <cat></cat>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        var superPowersMixin = {
            data(){
                return {
                    superPowers: false
                }
            },
            methods:{
                superMe(){
                    this.$el.classList.add("super");
                    this.superPowers = true;
                }
            },
            created(){
                this.$options.template = `<div><h3 v-show="superPowers">super</h3>`+ this.$options.template + `<button @click="superMe" v-if="!superPowers">Super!</button></div>`;
            }
        };

        Vue.component(
            'man',
            {
                template: '<p>👨🏻man</p>',
                mixins: [superPowersMixin]
            }
        );

        Vue.component(
            'cat',
            {
                template: '<p>🐱cat</p>',
                mixins: [superPowersMixin]
            }
        );

        new Vue({
            el: '#app'
        });


    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 13_Example_5.gif %}

## 範例(六)

使用component中的混合mixins。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-6</title>
</head>
<body>
    <div id="app">
        <greeter></greeter>
        <super-greeter></super-greeter>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        var Greeter = {
            template: '<p>{{message}}<button @click="greet">greet</button></p>',
            data () {
                return {
                    message: '...'
                }
            },
            methods: {
                greet () {
                    this.message = 'hello'
                }
            }
        };

        var SuperGreeter = {
            mixins: [Greeter],
            template: '<p>{{message}}<button @click="superGreet">supergreet</button></p>',
            methods: {
                superGreet () {
                    this.message = 'SUPER HELLO!';
                }
            }
        };

        new Vue({
            el: '#app',
            components: { Greeter, SuperGreeter }
        });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 13_Example_6.gif %}

## 範例(七)

在component裡更換slots區域更換。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-7</title>
</head>
<body>
    <div id="app">
        <framed>
            <cat :name="catName"></cat>
        </framed>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'framed',
            {
                template: 
                            `
                                <div class="frame">
                                    <h3>
                                        Russian cat mafia employee of the month
                                    </h3>
                                    <slot>
                                        Nothing framed.
                                    </slot>
                                </div>
                            `
            }
        );

        Vue.component(
            'cat',
            {
                template:
                            `
                                <div>
                                    <figure>
                                        <img src="http://placehold.it/220x220" />
                                        <figcaption>{{name}}</figcaption>
                                    </figure>
                                </div>
                            `,
                props: ['name']
            }
        );

        new Vue({
            el: '#app',
            data: {
                names: ['Murzik', 'Pushok', 'Barsik', 'Vaska', 'Matroskin']
            },
            computed:{
                catName(){
                    return this.names[Math.floor(Math.random() * this.names.length)] 
                }
            }
        });

    </script>
</body>
</html>

<style>
.frame{
  border: 5px dashed dodgerblue;
  width: 300px;
}
h3, figcaption{
  font-family: sans-serif;
  text-align: center;
  padding: 2px 0;
  width: 100%
}
</style>
~~~

### 網頁結果
{% asset_img 13_Example_7.gif %}

## 範例(八)

在component裡更換下方slots區域更換。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-8</title>
</head>
<body>
    <div id="app">
        <organogram>
            <div slot="boss">
              <figure>
                <img src="https://picsum.photos/210/210?image=1033" />
                <figcaption>Sylvester</figcaption>
              </figure>
            </div>
            <cat slot="employee" :name="catName"></cat>
          </organogram>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'organogram',
            {
                template: 
                            `
                                <div class="organogram">
                                    <h3>
                                        Scratchy co.
                                    </h3>
                                    <div class="boss">
                                        <h3>Boss</h3>
                                        <slot name="boss">No boss</slot>
                                    </div>
                                    <div class="employee">
                                        <h3>Employee</h3>
                                        <slot name="employee">No employee</slot>
                                    </div>
                                </div>
                            `
        });

        Vue.component(
            'cat',
            {
                template:
                        `
                            <div>
                            <figure>
                                <img src="https://picsum.photos/220/220/?random" />
                                <figcaption>{{name}}</figcaption>
                            </figure>
                            </div>
                        `,
                props: ['name']
        });

        new Vue({
            el: '#app',
            data: {
                names: ['Murzik', 'Pushok', 'Barsik', 'Vaska', 'Matroskin']
            },
            computed:{
                catName(){
                    return this.names[Math.floor(Math.random() * this.names.length)] 
                }
            }
        });

    </script>
</body>
</html>

<style>
.organogram{
  border: 5px dashed dodgerblue;
  width: 300px;
}
.boss{
  border: 5ps double mediumvioletred;
}
.employee{
  border: 2px outset lightgrey;
}
h3, figcaption{
  font-family: sans-serif;
  text-align: center;
  padding: 2px 0;
  width: 100%
}
</style>
~~~

### 網頁結果
{% asset_img 13_Example_8.gif %}

## 範例(九)

在component裡判斷更換slots區域更換。

>使用template scope 屬性，由scope屬性中取得object變數值，判斷哪一個slot做處理。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-9</title>
</head>
<body>
    <div id="app">
        <organogram>
            <template scope="props">
              <div v-if="props.type === 'boss'">
                <figure>
                  <img src="https://picsum.photos/210/210?image=1033" />
                  <figcaption>Sylvester</figcaption>
                </figure>
              </div>
              <div v-else-if="props.type === 'employee'"
                   :class="'r' + props.rank">
                <cat :name="catName"></cat>
              </div>
            </template>
          </organogram>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'organogram', 
            {
                template: 
                            `
                                <div class="organogram">
                                    <h3>Scratchy co.</h3>
                                    <div class="boss">
                                        <h3>Boss</h3>
                                        <slot type="boss">No boss</slot>
                                    </div>
                                    <div class="employee" v-for="rank in 2">
                                        <h3>Employee</h3>
                                        <slot type="employee" :rank="rank">No employee</slot>
                                    </div>
                                </div>
                            `
        });

        Vue.component(
            'cat',
            {
                template:
                            `
                                <div>
                                    <figure>
                                        <img src="https://picsum.photos/220/220/?random" />
                                        <figcaption>{{name}}</figcaption>
                                    </figure>
                                </div>
                            `,
                props: ['name']
        });

        new Vue({
            el: '#app',
            data: {
                names: ['Murzik', 'Pushok', 'Barsik', 'Vaska', 'Matroskin']
            },
            computed:{
                catName(){
                    return this.names[Math.floor(Math.random() * this.names.length)] 
                }
            }
        });

    </script>
</body>
</html>

<style>
.organogram{
  border: 5px dashed dodgerblue;
  width: 300px;
}
.boss{
  border: 5ps double mediumvioletred;
}
.employee{
  border: 2px outset lightgrey;
}
h3, figcaption{
  font-family: sans-serif;
  text-align: center;
  padding: 2px 0;
  width: 100%
}
.r1{
  font-size: 1.5em;
  color: red;
}
.r2{
  font-size: 1.2em;
  color: blue;
}
</style>
~~~

### 網頁結果
{% asset_img 13_Example_9.gif %}

## 範例(十)

使用自訂外部訊息。

> 提供command事件辨識字串，讓cancel、ok按個按鈕出發顯示資訊。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][13]component-10</title>
</head>
<body>
    <div id="app">
        <dialog-box command="confirmation" :cancellable="true" @cancel="msg = 'cancelled'" @ok="msg = 'confirmed'">
            <span slot="icon">⚠️</span>
            <span slot="message">Do you confirm?</span>
          </dialog-box>
        <p>OutPut: {{msg}}</p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        Vue.component(
            'dialog-box', 
            {
                template: 
                            `
                                <div>
                                    <div class="icon">
                                        <slot name="icon"></slot>
                                    </div>
                                    <slot class="message"></slot>
                                    <div class="buttons">
                                        <button v-if="cancellable" @click="cancel()">
                                            Cancel
                                        </button>
                                        <button @click="ok()">
                                            Ok
                                        </button>
                                    </div>
                                </div>
                            ` ,
                props:{
                    command: String,
                    cancellable: Boolean
                },
                methods:{
                    cancel(){
                        this.$emit('cancel', this.command)
                    },
                    ok(){
                        this.$emit('ok', this.command)
                    }
                }
            });

        new Vue({
            el: '#app',
            data:{
                msg: 'undefined'
            }
        });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 13_Example_10.gif %}
