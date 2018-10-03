---
title: '[VueJS][11][功能篇]-選單'
date: 2018-10-03 14:22:56
tags: VueJs
---

# 選單

* CheckBox
* Radio
* Select

<!--more-->

## CheckBox選單
### 語法

~~~html
<input type="checkbox" v-model="DataName" value="DataValue" />
~~~

> type: 指定checkbox。
> 
> DataName: 根據VueJs data屬性欄位中宣告之名稱。
> 
> DataValue: 選單內容。

### 範例(1-1)

顯示選擇選單內容

#### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][11]checkBox-1_1</title>
</head>
<body>
    <div id="app">
        <form>
            <fieldset>
                <lengend>What printers you want to use?</lengend><br>
                <label>
                    <input type="checkbox" v-model="outputPrinter" value="monochrome" />
                    Monochrome
                </label><br>
                <label>
                    <input type="checkbox" v-model="outputPrinter" value="plasma" />
                    Plasma Color
                </label><br>
                <label>
                    <input type="checkbox" v-model="outputPrinter" value="cloner" />
                    3D DNA Cloner
                </label><br>
            </fieldset>
        </form>
        {{outputPrinter}}
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                outputPrinter:[]
            }
        });

    </script>
</body>
</html>
~~~

#### 網頁結果
{% asset_img 11_Example_1-1.gif%}

### 範例(1-2)

點選Submit Button顯示選擇項目內容。

#### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][11]checkBox-1_2</title>
</head>
<body>
    <div id="app">
        <form>
            <fieldset>
                <lengend>What printers you want to use?</lengend><br>
                <label>
                    <input type="checkbox" v-model="outputPrinter" value="monochrome" />
                    Monochrome
                </label><br>
                <label>
                    <input type="checkbox" v-model="outputPrinter" value="plasma" />
                    Plasma Color
                </label><br>
                <label>
                    <input type="checkbox" v-model="outputPrinter" value="cloner" />
                    3D DNA Cloner
                </label><br>
                <input type="submit" value="Print now" @click.prevent="printHandler">
            </fieldset>
        </form>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                outputPrinter:[]
            },
            methods:{
                printHandler(){
                    let printers = this.outputPrinter;
                    alert('Printing with: ' + (printers.length ? printers.join(', ') : 'none') + '.');
                }
            }
        });

    </script>
</body>
</html>

~~~

#### 網頁結果
{% asset_img 11_Example_1-2.gif%}

## Radio選單
### 語法

~~~html
<input type="radio" v-model="DataName" value="DataValue" />
~~~

> type: 指定radio。
> 
> DataName: 根據VueJs data屬性欄位中宣告之名稱。
> 
> DataValue: 選單內容。

### 範例(2-1)

顯示選擇選單內容

#### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][11]Radio-2_1</title>
</head>
<body>
    <div id="app">
        <form>
            <fieldset>
                Choose your gender<br>
                <label>
                    <input type="radio" v-model="gender" value="male" />
                    Male
                </label><br>
                <label>
                    <input type="radio" v-model="gender" value="female" />
                    Female
                </label><br>
                <label>
                    <input type="radio" v-model="gender" value="alien" />
                    Alien
                </label><br>
            </fieldset>
        </form>
        <div>
            Choosen gender: '{{gender}}'
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                gender: undefined
            }
        });

    </script>
</body>
</html>
~~~

#### 網頁結果
{% asset_img 11_Example_2-1.gif%}

### 範例(2-2)

顯示選擇選單內容

#### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][11]Radio-2_2</title>
</head>
<body>
    <div id="app">
        <form>
            <fieldset>
                <legend>Today's animals</legend>
                <label>
                    <input type="radio" v-model="animal" :value="animals[i]" />
                    {{animals[i]}}
                </label><br>
                <label>
                    <input type="radio" v-model="animal" :value="animals[i+1]" />
                    {{animals[i+1]}}
                </label><br>
                <label>
                    <input type="radio" v-model="animal" :value="animals[i+2]" />
                    {{animals[i+2]}}
                </label><br>
                <input type="submit" value="Add to Farm" @click.prevent="addToFarm"></input>
            </fieldset>
        </form>
        <div>
            Choosen Animal: '{{animal}}' <br>
        <div>
            Your farm is compsed by {{farm.join(' ')}}
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                animals: ['🐖', '🐓', '🐄'],
                animal: undefined,
                farm: [],
                i: 0
            },
            methods:{
                addToFarm(){
                    if(this.animal === undefined){
                        return;
                    }
                    this.farm.push(this.animal);
                    this.animal = undefined;
                }
            }
        });

    </script>
</body>
</html>
~~~

#### 網頁結果
{% asset_img 11_Example_2-2.gif%}

## Select選單
### 語法

~~~html
<select v-model="DataName">
	<option>Item</option>
	...
</select>
~~~

> DataName: 根據VueJs data屬性欄位中宣告之名稱。
> 
> Item: 選單內容。

### 範例(3-1)

顯示選擇選單內容

#### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][11]Select-3_1</title>
</head>
<body>
    <div id="app">
        <form>
            <fieldset>
                <legend>Choose your country</legend>
                <label>
                    <select v-model="choosenCountry">
                        <option>Japan</option>
                        <option>Taiwan</option>
                        <option>Canada</option>
                    </select>
            </fieldset>
        </form>
        <div>
            Choosen: '{{choosenCountry}}' <br>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                choosenCountry: undefined
            }
        });

    </script>
</body>
</html>
~~~

#### 網頁結果
{% asset_img 11_Example_3-1.gif%}

### 範例(3-2)

使用v-for顯示選單內容。

#### 網頁Html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>[VueJS][11]Select-3_2</title>
</head>
<body>
    <div id="app">
        <form>
            <fieldset>
                <legend>Choose your country</legend>
                <label>
                <select v-model="choosenCountry">
                    <option v-for="opt in options" :value="opt.value">{{opt.text}}</option>
                 </select>
            </fieldset>
        </form>
        <div>
            Choosen: '{{choosenCountry}}' <br>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.js"></script>

    <script>
    
        new Vue({
            el: '#app',
            data:{
                choosenCountry: undefined,
                options: [
                    { text: 'Taiwan', value: 'TW' },
                    { text: 'Japan' , value: 'JP' },
                    { text: 'Canada', value: 'CA' }
                ]
            }
        });

    </script>
</body>
</html>
~~~

#### 網頁結果
{% asset_img 11_Example_3-2.gif%}