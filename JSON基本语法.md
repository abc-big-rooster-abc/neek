# JSON基本语法

## json的顶层支持三种类型的值

### 简单值：数字(Number),字符串(String,不支持单引号)，布尔类型(Boolean),null类型；

### 对象值：由key,value组成，key是字符串类型，并且必须添加双引号，值可以是简单值，对象值，数组值

### 数组值：数组的值可以是简单值、对象值、数组值



## JSON.stringfy(obj)     

~~~js
obj = {
    name:"谢公胜",
    age:18,
    friend:{
        name:"kobe",
        hobbies:["篮球","足球"]
    }

}

// 将obj转变为 json 格式的字符串
const objString = JSON.stringify(obj)

console.log(objString)

// 将对象数据存储localStorage
localStorage.setItem("obj",obj)
console.log("将对象直接存在localStorage中：",localStorage.getItem("obj"))

// 将对象数据存储localStorage
localStorage.setItem("obj",objString)
console.log("将对象转为json字符串形式：",localStorage.getItem("obj"))




Peflect.js:14 {"name":"谢公胜","age":18,"friend":{"name":"kobe","hobbies":["篮球","足球"]}}
Peflect.js:18 将对象直接存在localStorage中： [object Object]
Peflect.js:22 将对象转为json字符串形式： {"name":"谢公胜","age":18,"friend":{"name":"kobe","hobbies":["篮球","足球"]}}
~~~



## JSON.parse(jsonString)  将JSON格式的字符串转回对象

~~~js
obj = {
    name:"谢公胜",
    age:18,
    friend:{
        name:"kobe",
        hobbies:["篮球","足球"]
    }

}

// 将obj转变为 json 格式的字符串
const objString = JSON.stringify(obj)
console.log("对象转为json字符串：",objString)

const obj1 = JSON.parse(objString)
console.log("json字符串转为对象形式：",obj1)




[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
对象转为json字符串： {"name":"谢公胜","age":18,"friend":{"name":"kobe","hobbies":["篮球","足球"]}}
json字符串转为对象形式： {
  name: '谢公胜',
  age: 18,
  friend: { name: 'kobe', hobbies: [ '篮球', '足球' ] }
}

[Done] exited with code=0 in 0.26 seconds

~~~



## JSON.stringfy第二个参数用法 ，选择性转换

~~~js
obj = {
    name:"谢公胜",
    age:18,
    friend:{
        name:"kobe",
        hobbies:["篮球","足球"]
    }

}

// stringfy 第二个参数replacer
// 传入数组：设定哪些是需要转换
const a = JSON.stringify(obj,['name','friend'])
console.log(a)



[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
{"name":"谢公胜","friend":{"name":"kobe"}}

[Done] exited with code=0 in 0.244 seconds

~~~



## JSON.stringfy第二个参数用法 ，也可以传入函数对原对象修改

~~~js
obj = {
    name:"谢公胜",
    age:18,
    friend:{
        name:"kobe",
        hobbies:["篮球","足球"]
    }

}

const a = JSON.stringify(obj,function(key,value){
    if(key === 'age'){
        return value + 1
    }
    return value
})
console.log(a)



[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
{"name":"谢公胜","age":19,"friend":{"name":"kobe","hobbies":["篮球","足球"]}}

[Done] exited with code=0 in 0.268 seconds


~~~

## JSON.stringfy第三个参数用法 ，space增加空格，增强可读性

~~~js
obj = {
    name:"谢公胜",
    age:18,
    friend:{
        name:"kobe",
        hobbies:["篮球","足球"]
    }

}
// 第三个参数 space 
const a = JSON.stringify(obj,null,2)
console.log(a)



[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
{
  "name": "谢公胜",
  "age": 18,
  "friend": {
    "name": "kobe",
    "hobbies": [
      "篮球",
      "足球"
    ]
  }
}

[Done] exited with code=0 in 0.307 seconds
~~~

## 浅拷贝原理  const  info1 = {...obj}    const info2 = obj.assign()

![image-20220614000304724](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220614000304724.png)

## 深拷贝

~~~js
obj = {
    name:"谢公胜",
    age:18,
    friend:{
        name:"kobe",
        hobbies:["篮球","足球"]
    }

}
// 深拷贝
const a = JSON.stringify(obj)
const b = JSON.parse(a)
obj.friend.name = '小三'
console.log(obj.friend.name)
console.log(b.friend.name)


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
小三
kobe

[Done] exited with code=0 in 0.258 seconds

~~~

