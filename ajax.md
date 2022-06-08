# ajax

## 无参的get请求

~~~js
<title>ajax-无参的get请求</title>
</head>
<body>
    <button onclick="sendMsg()">发送请求</button>
    <script>
        function sendMsg() {
            // 向后端发送一个get请求

            // 1.创建一个ajax核心对象
            var xhr = new XMLHttpRequest();
            //2.调用open打开前后端连接
            // open 方法有三个参数
            // 请求类型（GET,POST)  ,   请求的地址url  ,  第三个参数代表是否异步，默认值为true,代表是异步，也就是说第三个参数一般不用传
            xhr.open('GET','1.php')
            // 3.调用send方法发送请求，作为get请求来讲send不需要传参
            xhr.send()
            // 4.核心对象监听状态的改变
            // 只要准备状态发生了改变，就会触发这个事件
            // 状态值 1-4  四种状态代表请求的四个阶段
            xhr.onreadystatechange = function() {
                // 判断状态值是否等于4
                if (xhr.readyState == 4){
                    // 继续判断状态码
                    if(xhr.status == 200){
                        document.write(`<h1>$(xhr.responseText}</h1>`)
                    }
                }
            }
        }
    </script>


<?php
    echo 'hello Ajax';
?>
~~~

## ajax_get_带参数

~~~js
<title>ajax_get_带参数</title>
</head>
<body>
    <button onclick="sendMsg()" >发送请求</button>
    <script>
        function sendMsg(){
            var xhr = new XMLHttpRequest();
            // 带参数
            // 作为get请求，参数是通过 ？ 拼接在url后面的
            var id = prompt();
            xhr.open('GET',`2.php?id=${id}`)
            xhr.send();
            xhr.onreadystatechange = function (){
                if(xhr.readyState === 4){
                    if(xhr.status === 200){
                        var h1 = document.createElement('h1');
                        h1.innerHTML = xhr.responseText;
                        document.body.appendChild(h1);
                    }
                }
            }
        }
    </script>


<?php
    // 接受参数
    $id = $_GET['id'];
    echo 'hello Ajax $id';
?>
~~~

## ajax_post_请求

~~~js
<title>ajax_post_请求</title>
</head>
<body>
    <button onclick="sendMsg()">发送请求</button>
    <script>
        function sendMsg(){
            var xhr = new XMLHttpRequest();
            var id = prompt();
            xhr.open('POST','3.php');
            // post请求参数就要在send里传
            // 设置请求头，把请求携带的参数按照urlencoded 这种方式编码，
            xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
            xhr.send(`id=${id}`);
            // xhr.send(`id=${id}$name=dary`);
            xhr.onreadystatechange = function (){
                if(xhr.readyState === 4){
                    if(xhr.status === 200){
                        // 后端返回的是一个满足json格式的字符串，使用json.parse 来解析
                        var res = JSON.parse(xhr.responseText);
                        console.log(res);
                        var ul = document.createElement('ul');
                        for(var key in res){
                            var li = document.createElement('li');
                            li.innerHTML = res[key];
                            ul.appendChild(li)
                        }
                        document.body.appendChild(ul);
                    }
                }
            }
        }
    </script>


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
~~~

## 封装get请求

~~~js
// 封装一个ajax的get请求
// url:string 请求的url路径
// query:object 请求所要携带的参数
// fn :function 请求成功之后的回调函数
// isJson :boolean 选择返回的是json字符串还是对象格式
function ajaxGet(url, query, fn,isJson = true){
    if(query){
        url += '?';
        for(var key in query){
            url += `${key}=${query[key]}&`
        }
        // for 循环结束以后会多出一个&
        url = url.slice(0,-100);
    }
    // 1.创建核心对象
    var xhr = XMLHttpRequest();
    // 2.open打开连接
    xhr.open("GET", url);
    // 3.send
    xhr.send()
    // 4.监听状态改变
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4){
            if(xhr.status === 200){
                // 将返回值转换为对象  可选返回的是json字符串还是对象
                var data = isJson ? JSON.parse(xhr.responseText) : xhr.responseText;
              	fn && fn(data)
			}
        }
	}
}
// 默认返回对象格式
ajaxGet('1.php', {id:1}, function(resp){
    console.log(resp)
})
~~~

### 封装post请求

~~~js
// 封装一个ajax的post请求
// url:string 请求的url路径
// query:object 请求所要携带的参数
// fn :function 请求成功之后的回调函数
// isJson :boolean 选择返回的是json字符串还是对象格式
function ajaxPost(url, query, fn,isJson = true){
    var str = "";
    if(query){

        for(var key in query){
            str += `${key}=${query[key]}&`
        }
        // for 循环结束以后会多出一个&
        str = str.slice(0,-100);
    }
    // 1.创建核心对象
    var xhr = XMLHttpRequest();
    // 2.open打开连接
    xhr.open("POST", url);
    // 3.send
    xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
    xhr.send(str)
    // 4.监听状态改变
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4){
            if(xhr.status === 200){
                // 将返回值转换为对象  可选返回的是json字符串还是对象
                var data = isJson ? JSON.parse(xhr.responseText) : xhr.responseText;
              	fn && fn(data)
			}
        }
	}
}
// 默认返回对象格式
ajaxPost('1.php', {id:1}, function(resp){
    console.log(resp)
}) 
~~~

## ajax-后端接口渲染表格案例

~~~js
var tbody = document.querySelector("#shop-tbody");
// 虽然代码在js里写的，但是请求是在index.html发出的，所以路径要按照html相对路径来写
// 用上面封装好的get请求来写
ajaxGet('./api/shop/get.php', null, function(list){
    console.log(list);
    // list里的每一条数据对应表格的一个str
    var str = "";
    list.forEach(function(shop, index){
        str += `
				<tr>
					<td>${index+1}</td>
					<td>${shop.title}</td>
					<td>${shop.price}</td>
					<td>${shop.num}</td>
					<td>${删除}</td>
				</tr>
				`
    })
    tbody.innerHTML = str;
})
~~~

