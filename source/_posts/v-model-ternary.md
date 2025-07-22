---
title: v-model与三元表达式
date: 2025-7-21
tags: vue
categories: vue
---

# v-model和三元表达式
**在** **v-model** **使用三元运算符绑定数据时，比如** `v-model="name === '' ? text : name"`**，代码逻辑为** **name** **字段是空字符串时，**  **input框** **绑定** **text** **字段，但是这样会报错。可以采取** `computed` **方式：**


``` js
<input type="text" v-model="XXX">

computed:{
    xxx(){
        if(this.name){
            return this.text;
        }else{
            return this.name;
        }
    }
}
```
