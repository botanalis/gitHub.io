---
title: '[VueJS][06][功能篇]-運算'
date: 2018-09-29 15:44:35
tags: VueJs
---

# 即時運算

使用 Vue `computed ` 宣告處理Method。

##語法
~~~html
new Vue({
  computed:{
          functionName(){}
  }
});
~~~

> computed為VueJS的屬性欄位，在裡面宣告要執行的function。

<!--more-->

## 範例 (一) 即時處理

即時顯示二個input處理結果

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][06]computed-1</title>
</head>
<body>
    <div id="app">
            <input type="text" v-model="firstName" />
            <input type="text" v-model="lastName" />
            <p><output>{{computedFullName}}</output></p>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                firstName: 'John',
                lastName: 'show'
            },
            computed:{
                computedFullName(){
                    return this.firstName + ' ' + this.lastName;
                }
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 06_Example_1.gif %}

## 範例 (二) 過濾清單中的資料

將data中的資料進行篩選後顯示出 **field** 不是 **Physics** 字串結果。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][06]computed-2</title>
</head>
<body>
    <div id="app">
        <h3>List of ecpensive experiments</h3>
        <ul>
            <li v-for="exp in nonPhysics">
                {{exp.name}}  ({{exp.cost}}m 💲)
            </li>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                experiments:[
                    {
                        name: 'RHIC Ion Collider', 
                        cost: 650, 
                        field: 'Physics'
                    },
                    {
                        name: 'Neptune Undersea Observatory', 
                        cost: 100, 
                        field: 'Biology'
                    },
                    {
                        name: 'Violinist in the Metro', 
                        cost: 3, 
                        field: 'Psychology'
                    },
                    {
                        name: 'Large Hadron Collider', 
                        cost: 7700, 
                        field: 'Physics'
                    },
                    {
                        name: 'DIY Particle Detector', 
                        cost: 0, 
                        field:'Physics'
                    }
                ]
            },
            computed:{
                nonPhysics(){
                    return this.experiments.filter(
                    exp => exp.field !== 'Physics');
                }
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 06_Example_2.png %}

## 範例 (三) Methods與Computed相同執行結果
呼叫Methods與Computed的執行結果。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][06]computed-3</title>
</head>
<body>
    <div id="app">
        <h3>List of ecpensive experiments</h3>
        <ul>
            <li v-for="exp in filteredExperiments">
                {{exp.name}}  ({{exp.cost}}m 💲)
            </li>
        </ul>
            
        <h3>List of ecpensive experiments(filter)</h3>
        <ul>
            <li v-for="exp in nonPhysics(lowCost(experiments))">
                {{exp.name}}  ({{exp.cost}}m 💲)
            </li>
        </ul>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                experiments:[
                    {
                        name: 'RHIC Ion Collider', 
                        cost: 650, 
                        field: 'Physics'
                    },
                    {
                        name: 'Neptune Undersea Observatory', 
                        cost: 100, 
                        field: 'Biology'
                    },
                    {
                        name: 'Violinist in the Metro', 
                        cost: 3, 
                        field: 'Psychology'
                    },
                    {
                        name: 'Large Hadron Collider', 
                        cost: 7700, 
                        field: 'Physics'
                    },
                    {
                        name: 'DIY Particle Detector', 
                        cost: 0, 
                        field:'Physics'
                    }
                ]
            },
            computed:{
                filteredExperiments(){
                return this.lowCost(this.nonPhysics(this.experiments));
                }
            },
            methods:{
                nonPhysics(list){
                    return list.filter(exp => exp.field !== 'Physics');
                },
                lowCost(list){
                    return list.filter(exp => exp.cost <= 3);
                }
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 06_Example_3.png %}

## 範例 (四) 排序清單中的資料
將data中的資料進行排序後顯示出結果。

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][06]computed-4</title>
</head>
<body>
    <div id="app">
        <table border="1">
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Country</th>
                    <th>Electricity</th>
                </tr>
            </thead>
                <tr v-for="dam in damsByElectricity">
                    <td>{{dam.name}}</td>
                    <td>{{dam.country}}</td>
                    <td>{{dam.electricity}}</td>
                </tr>
        </table>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                dams:[
                    {
                        name: 'Nurek Dam', 
                        country: 'Tajikistan', 
                        electricity: 3200
                    },
                    {
                        name: 'Three Gorges', 
                        country: 'China', 
                        electricity: 22500
                    },
                    {
                        name: 'Tarbela Dam', 
                        country: 'Pakistan', 
                        electricity: 3500
                    },
                    {
                        name: 'Guri Dam', 
                        country: 'Venezuela', 
                        electricity: 10200
                    }
                ]
            },
            computed:{
                damsByElectricity(){
                    return this.dams.sort( (d1, d2) => d2.electricity - d1.electricity );
                }
            }
        });
    </script>
</body>
</html>
~~~

### 網頁結果
{% asset_img 06_Example_4.png %}

## 範例 (五) 動態排序清單中的資料
點選欄位更變排序方式（ **遞增** or **遞減** ）

### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][06]computed-5</title>
</head>
<body>
    <div id="app">
        <table  border="1">
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Country</th>
                    <th v-bind:class="order ===1 ? 'descending' : 'ascending'"
                        @click="sort">Electricity
                    </th>
                </tr>
            </thead>
                <tr v-for="dam in damsByElectricity">
                    <td>{{dam.name}}</td>
                    <td>{{dam.country}}</td>
                    <td>{{dam.electricity}}</td>
                </tr>
        </table>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                dams:[
                    {
                        name: 'Nurek Dam', 
                        country: 'Tajikistan', 
                        electricity: 3200
                    },
                    {
                        name: 'Three Gorges', 
                        country: 'China', 
                        electricity: 22500
                    },
                    {
                        name: 'Tarbela Dam', 
                        country: 'Pakistan', 
                        electricity: 3500
                    },
                    {
                        name: 'Guri Dam', 
                        country: 'Venezuela', 
                        electricity: 10200
                    }
                ],
                order: 1
            },
            computed:{
                damsByElectricity(){
                    return this.dams.sort( (d1, d2) => (d2.electricity - d1.electricity) * this.order);
                }
            },
            methods:{
                sort(){
                    this.order = this.order * -1;
                }
            }
        });
    </script>
</body>
</html>

<style>
.ascending:after{
  content: "\25B2";
}
.descending:after{
  content: "\25BC";
}
</style>
~~~

### 網頁結果
{% asset_img 06_Example_5.gif %}
