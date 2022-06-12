# Promise面试题

~~~js
setTimeout(function(){
    console.log("setTimeout1");
    new Promise(function(resolve){
        resolve();
    }).then(function(){
        new Promise(function(resolve){
            resolve()
        }).then(function(){
            console.log("then4");
        });
        console.log("then2")
    })
})


new Promise(function(resolve){
    console.log("promise1")
    resolve()
}).then(function(){
    console.log("then1");
});

setTimeout(function(){
    console.log("setTimeout2");
});

console.log(2);

queueMicrotask(()=>{
    console.log("queueMicrotask1")
});

new Promise(function(resolve){
    resolve();
}).then(function(){
    console.log("then3")
})


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
promise1
2
then1
queueMicrotask1
then3
setTimeout1
then2
then4
setTimeout2

[Done] exited with code=0 in 0.254 seconds
~~~

### mian script                  微任务                        宏任务

promise1                                           new Promise()...                           function(){}

2                                                           then4                                             setTimeout2

then1                                                                    

queueMicrotask1

then3

setTimeout1

then2





~~~js
async function bar(){
    // 第二执行  bar() 立即执行 和cons.log("11111")是同一个代码块
    console.log("22222222222222")
    return new Promise((resolve)=>{
        resolve()
    })
}

async function foo(){
    // 一调用直接执行，不会做异步处理 在await 后面接promise时才算异步，到微任务里面
    console.log("111111")
    await bar()
    console.log("333333")
}

foo()
console.log("44444444444")


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
111111
22222222222222
44444444444
333333

[Done] exited with code=0 in 0.276 seconds

~~~





~~~js
async function async1(){
    console.log("async1 start")
    await async2();
    console.log("async1 end")
}


async function async2(){
    console.log("async2")
  
}
console.log("script start")

setTimeout(function(){
    console.log("settimeOUt")
},0)

async1();

new Promise(function(resolve){
    console.log('promise1')
    resolve();
}).then(function(){
    console.log("promise2")
})

console.log("script end")

[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
script start
async1 start
async2
promise1
script end
async1 end
promise2
settimeOUt

[Done] exited with code=0 in 0.319 seconds
~~~

