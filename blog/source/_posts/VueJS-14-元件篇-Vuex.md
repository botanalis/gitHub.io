---
title: '[VueJS][14][元件篇]-Vuex'
date: 2018-10-09 00:06:23
tags: VueJs
---

# Vuex狀態管理

Vuex提供一個可以儲存狀態的框架，可以讓Component與其他Component藉由宣告Vuex進行狀態管理以及處理變化。

<!--more-->

## 單向個體資料狀態
由於每個Component都是各自獨立，每個都有自己的資料狀態以及處理流程，每個運作如下：

~~~javascript
new Vue({
  // state
  data () {
    return {
      count: 0
    }
  },
  // view
  template: `
    <div>{{ count }}</div>
  `,
  // actions
  methods: {
    increment () {
      this.count++
    }
  }
})
~~~

宣告Vue Object出來時，分為「state」、「actions」、「view」:

>state：資料來源。
>
>actions：反映在View上的使用者操作處理。
>
>view：敘述方式將state映射到View。

{% asset_img 14_Content_1.png %}

圖取自[官網](https://vuex.vuejs.org/zh/)

由於要讓多個Component分享資料狀態時，回破壞原先Component的單純化的特性，演變最後提供多個Method來取得內部資料，以及複製多個Object來分享資料，變得不容易維護了，Vue提供Vuex來進行通一管理，Vuex架構如下：

{% asset_img 14_Content_2.png %}

圖取自[官網](https://vuex.vuejs.org/zh/)

## Vuex語法

每一個Vuex都是一個store（倉庫），Vuex提供[state]來宣告要共用的參數(不提供外部直接存取)、[mutations]來宣告提供commit呼叫使用。

~~~html
const store = new Vuex.Store({
    state:{
       count: 0,
       ....
    },
    mutations:{
       `function Name` (state){
                ....
        },
       `function Name2` (state, parament_1, ...){
        }    
    }
});
//外部呼叫
store.commit('function Name');
store.commit('function Name2', 參數_1)
~~~

## 範例(一)

Vuex統一管理狀態顯示字串。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][14]Vuex-1</title>
</head>
<body>
    <div id="app">
        <blabber></blabber>
        <blabber></blabber>
        <script src="https://unpkg.com/vuex"></script>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        const store = 
            new Vuex.Store({
                    strict: true,
                    state:{
                    currentActor: -1,
                    currentLine: -1,
                    actors:[],
                    dialogue:[
                        'Where are you going?',
                        'To the cinema',
                        'What`s on at the cinema?',
                        'Quo vadis?',
                        'Oh, what does it mean?'
                    ]
                },
                mutations:{
                    entersScene (state, uuid) {
                        state.currentLine = ( state.currentLine + 1) % state.dialogue.length;
                        state.actors.push({
                            uuid: uuid,
                            line: state.dialogue[state.currentLine]
                        });
                        state.currentActor = (state.currentActor + 1) % state.actors.length;
                    },
                    nextLine (state) {
                        state.currentActor = (state.currentActor + 1) % state.actors.length;
                        state.currentLine = (state.currentLine + 1) % state.dialogue.length;
                        state.actors[state.currentActor].line = state.dialogue[state.currentLine];
                    }
                }
            });
        Vue.component(
            'blabber',
            {
                template: "<p>{{currentLine}}</p>",
                data(){
                    return {
                        uuid: Math.random()
                    }
                },
                computed:{
                    currentLine(){
                        return store.state.actors.find(actor => actor.uuid === this.uuid).line;
                    }
                },
                created(){
                    store.commit('entersScene', this.uuid);
                }
        });

    new Vue({
        el:'#app',
        mounted(){
            setInterval(() => store.commit('nextLine'), 2000);
        }
    });

    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 14_Example_1.gif %}