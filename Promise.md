# Promise

## 原始实现异步请求处理

~~~js

// 原始实现异步请求处理

function requestData(url,successCallback, failCallback){
    setTimeout(()=>{
        //模拟网络请求
        if (url === 'coderwhy'){
            let names = ['adb','dd']
            successCallback(names)
        }
        else{
            let errMessage = '亲求失败';
            failCallback(errMessage)
        }
    },1000)
};
const a = requestData('coderwhy',(a)=>{
    console.log(a)
},
(b)=>{
    console.log(b)
})

const b = requestData('谢公胜',(a)=>{
    console.log(a)
},
(b)=>{
    console.log(b)
})

[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
[ 'adb', 'dd' ]
亲求失败

[Done] exited with code=0 in 1.237 seconds
~~~

## Promise实现异步请求

~~~js
function requestData(url){
return new Promise((resolve, reject)=>{
    setTimeout(()=>{
        //模拟网络请求
        if(url === 'coderwhy'){
            let names = ['adb','dd']
            resolve(names)
        }
        else{
            let errMessage = '亲求失败';
            reject(errMessage)
        }
    },1000)  
})
}
// 方法1
const promist_1 = requestData('coderwhy')
promist_1.then((a)=>{
    console.log(a)
}).catch((b)=>{
    console.log(b)
}).finally(()=>{
    console.log("我都会执行1")
})
// 方法2
promist_1.then((a)=>{
    console.log(a)
},  (b)=>{
    console.log(b)
}).finally(()=>{
    console.log("我都会执行2")
})


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
[ 'adb', 'dd' ]
[ 'adb', 'dd' ]
我都会执行2
我都会执行1 
~~~









~~~js
// 之所以使用Promise,只是为了不写回调函数，无线套娃，为了把本来异步的代码写成同步的形式，方便阅读
// resolve 代表成功，承诺兑现
// reject  代表失败  承诺失信
  const pro = new Promise((resolve, reject) => {
      //许下承诺写一个异步代码
      setTimeout(() => {
          // 一秒之后产生的随机数 大于0.5
          const num = Math.random();
          if(num > 0.5){
              //承诺兑现
              resolve(num);
          }else{
              reject(num);
          }
      },1000)
  });
// 现在承诺兑现或者失败的事情不用再回调函数里写了，而是then catch 
// 把异步代码写成同步形式
// catch 和 finally不是必写的
  pro.then((n) => {
      // 这里要写的就是承诺兑现之后的代码
      console.log("承诺兑现，num大于0.5的"+n)
  }).catch((n) => {
      console.log("承诺失败，num小于等于0.5的"+n)
  }).finally(() => {
      // 无论成功还是失败都会执行这里的代码
      console.log("无论num大不大于0.5,都会执行")
  })

// Promise 有三种状态
Pending(进行中，初始状态，即不是成功，也不是失败状态）
Resolved(又称Fulfilled,意味着操作成功完成）
Rejected(意味着操作失败)
~~~

## 封装一个基于promise的ajax get请求

~~~js
    <script>
        function promise_get (url, query, isJson=true){
            if(query){
                // 如果有参数
                url += '?';
                for(var key in query){
                    url += `${key}=${query[key]}&`
                }
                // for 循环结束以后会多出一个&
                url = url.slice(0,-1);
            }
            return new Promise((resolve, reject) => {
                // 这里代表刚许下承诺，promise处于pending状态
                var img = document.createElement('img');
                img.src="../i.png";
                document.body.append(img)
                // 许下一个异步承诺
                // 承诺ajax请求发出去将来一定会得到响应
                var xhr = new XMLHttpRequest()
                xhr.open('GET', url);
                xhr.send()
                xhr.onreadystatechange = function () {
                    if(xhr.readyState === 4){
                        if(xhr.status === 200){
                            var data = isJson ? JSON.parse(xhr.responseText) : xhr.responseText;
                            resolve(data);
                        }
                        else{
                            reject();
                        }
                        // 
                        document.body.removeChild(img)
                    }
                }
            })
        }
        var pro = promise_get('3.php', {id:3});
        pro.then(resp => {
            console.log(resp)     // {id:3,title:"水杯"，price:2000}
        })

        <?php
        // 接受参数
        $id = $_POST['id'];
        // 根据$id 去查找不同的数据
        // 模拟一下
        $arr = array(
            "id" => $id,
            "title" => "键盘",
            "price" =>  2000

        );
        echo json_encode($arr)
    ?>
    </script>
~~~

## promise-嵌套

~~~js
    <title>promise嵌套</title>
</head>
<body>
    <script>
        // 第一种方法
        // new Promise((resolve, reject) => {
        //     setTimeout(() => {
        //         var num = Math.random();
        //         if(num > 0.5){
        //             resolve();
        //         }
        //         else{
        //             reject()
        //         }
        //     },1000)
        // }).then(() => {
        //     // 代码第一个promise成功
        //     new Promise((resolve, reject) => {

        //     }).then(() => {

        //     })
        // })

        // 第二种方法
        new Promise((resolve, reject) => {
            setTimeout(() => {
                var num = Math.random();
                if(num > 0.5){
                    resolve();
                }
                else{
                    reject()
                }
            },1000)
        }).then(() => {
            // 代码第一个promise成功
            // 许下第二个承诺的时候把promise return 出去
            return new Promise((resolve, reject) => {

            })
        }).then(() => {
                // 这里的代码是第二个promise resolve以后执行
    })
    </script>
~~~

## Promise案例

~~~js
<title>promise_案例</title>
</head>
<body>
    <script>
                //做饭
        function cook(){
            console.log('开始做饭。');
            var p = new Promise(function(resolve, reject){        //做一些异步操作
                setTimeout(function(){
                    console.log('做饭完毕！');
                    resolve('鸡蛋炒饭');
                }, 1000);
            });
            return p;
        }
        
        //吃饭
        function eat(data){
            console.log('开始吃饭：' + data);
            var p = new Promise(function(resolve, reject){        //做一些异步操作
                setTimeout(function(){
                    console.log('吃饭完毕!');
                    resolve('一块碗和一双筷子');
                }, 2000);
            });
            return p;
        }
        
        function wash(data){
            console.log('开始洗碗：' + data);
            var p = new Promise(function(resolve, reject){        //做一些异步操作
                setTimeout(function(){
                    console.log('洗碗完毕!');
                    resolve('干净的碗筷');
                }, 2000);
            });
            return p;
        }
        cook()
        .then(function(data){
            return eat(data);
        })
        .then(function(data){
            return wash(data);
        })
        .then(function(data){
            console.log(data);
        });
        // 开始做饭。
        // promise_案例.html:16 做饭完毕！
        // promise_案例.html:25 开始吃饭：鸡蛋炒饭
        // promise_案例.html:28 吃饭完毕!
        // promise_案例.html:36 开始洗碗：一块碗和一双筷子
        // promise_案例.html:39 洗碗完毕!
        // promise_案例.html:53 干净的碗筷
    </script>
~~~

## 当resolve传入的是一个promise时，以这个promise里面的状态为准，

![image-20220611153239053](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220611153239053.png)

## 传入一个对象，这个兑现有then方法

![image-20220611153455918](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220611153455918.png)