# async  await

~~~js

// 书写方式
async function foo(){

}

const foo2 = async () =>{

}

class Foo{
    async bar(){

    }
}

async function foo(){
    console.log("111111")
    console.log("222222")
    console.log("3333333")
}
console.log("script start")
foo()
console.log("script end")

[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
111111
222222
3333333
script end

[Done] exited with code=0 in 0.315 seconds

~~~

## 和普通函数的区别



## 直接返回一个值

~~~js
// 异步函数的返回值一定是一个Promise
async function foo(){
    console.log("start")
    console.log("中间代码")
    console.log("end")
}
console.log("script start")
const promise = foo()
promise.then(res =>{
    console.log("promise then funcion exex:", res)   // 没有返回值相当于返回underfined
})


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
start
中间代码
end
promise then funcion exex: undefined

[Done] exited with code=0 in 0.246 seconds





// 异步函数的返回值一定是一个Promise
async function foo(){
    console.log("start")
    console.log("中间代码")
    console.log("end")
    return 1
}
console.log("script start")
const promise = foo()
promise.then(res =>{
    console.log("promise then funcion exex:", res)   // 没有返回值相当于返回underfined
}) 	  	


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
start
中间代码
end
promise then funcion exex: 1

[Done] exited with code=0 in 0.232 seconds
~~~





##  返回thenablse

~~~js
// 异步函数的返回值一定是一个Promise
async function foo(){
    console.log("start")
    console.log("中间代码")
    console.log("end")
    
    // 返回thenablse
    return {
        then: function(resolve, reject){
            resolve("hahahhah")
        }
    }
}
console.log("script start")
const promise = foo()
promise.then(res =>{
    console.log("promise then funcion exex:", res)  
}) 	
console.log("我不该在最后")


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
start
中间代码
end
我不该在最后
promise then funcion exex: hahahhah

[Done] exited with code=0 in 0.226 seconds
~~~



## 返回一个Promise

~~~js
// 异步函数的返回值一定是一个Promise
async function foo(){
    console.log("start")
    console.log("中间代码")
    console.log("end")
    return new Promise((resolve, reject) => {
        setTimeout(()=>{
            resolve("heheheheh")
        }, 2000)
    })
}
console.log("script start")
const promise = foo()
promise.then(res =>{
    console.log("promise then funcion exex:", res)  
})
console.log("我该不该在最后")


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
start
中间代码
end
我该不该在最后
promise then funcion exex: heheheheh

[Done] exited with code=0 in 2.243 seconds
~~~

## 抛出异常

~~~js
// 异步函数的返回值一定是一个Promise
async function foo(){
    console.log("start")
    console.log("中间代码")
    throw new Error("error message")
    console.log("end")

}
console.log("script start")
foo()
console.log("你好啊")



[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
start
中间代码
你好啊
c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js:5
    throw new Error("error message")
          ^

Error: error message
    at foo (c:\Users\root
~~~





## 抛出的异常，就是promise 里的reject 用catch接受

~~~js
// 异步函数的返回值一定是一个Promise
async function foo(){
    console.log("start")
    console.log("中间代码")
    throw new Error("error message")
    console.log("end")

}
console.log("script start")
const a = foo()
a.catch(function(err){
    console.log("错误提示为：", err)
})
console.log("我不是最后执行的")





[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
start
中间代码
我不是最后执行的
错误提示为： Error: error message
    at foo (c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js:5:11)
    at Object.<anonymous> (c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js:10:11)
    at Module._compile (node:internal/modules/cjs/loader:1105:14)
~~~





# await关键字

## async函数另外一个特殊之处就是可以在他的内部使用 await关键字 而普通函数不可以

## @ await 关键字特点： 通常使用await时后面会跟一个表达式，这 个表达式会返回一个promise

## await会等到Promise的状态变成fulfilled状态之后，继续执行异步函数

## 如果await后面是一个普通的值，那么会直接返回这个值

## 如果await后面是一个thenable的对象，那么会根据对象的then方法调用后来决定后续的值



## await 不执行 后面都不会指向(可以看成await后面then的执行语句)

## await 后面接表达式

~~~js
function requestData(){
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve(22222)
        },2000)
    })
}

async function foo(){
    const a = await requestData()
    console.log(a)
    console.log("qqqqqqqqqqqqqqqq")
}


foo()
console.log("-------------")



[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
-------------
22222
qqqqqqqqqqqqqqqq

[Done] exited with code=0 in 2.238 seconds

~~~





## await 后面跟其他的值

~~~js
async function foo(){
    console.log("我是最开始的")
    const a = await 11111
    console.log(a)
    console.log("qqqqqqqqqqqqqqqq")
}


foo()
console.log("-------------")



[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
我是最开始的
-------------
11111
qqqqqqqqqqqqqqqq

[Done] exited with code=0 in 0.228 seconds
~~~





## reject

~~~js
async function foo(){
    console.log("我是最开始的")
    const a = await new Promise((resolve,reject)=>{
        reject("111111111111111111")
    })
    console.log(a)
    console.log("qqqqqqqqqqqqqqqq")
}


foo().catch((err)=>{
    console.log("错误提示：", err)
})
console.log("-------------")


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
我是最开始的
-------------
错误提示： 111111111111111111

[Done] exited with code=0 in 0.223 seconds
~~~

