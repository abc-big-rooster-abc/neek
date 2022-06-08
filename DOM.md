# DOM

~~~js
//1. getElementsByClassName 根据类名获得某些元素集合
var boxs = document.getElementsByClassName('box');
// 2. querySelector 返回指定选择器的第一个元素对象 切记 里面的选择器需要加符号 .box #nav
var firstBox = document.querySelector('.box');
var li = document.querySelector('li');
// 3.querySelectorAll() 返回指定选择器的所有元素对象集合
var allBox = document.querySelectorAll('.box');

// 获取特殊元素（body html)
document.body // 返回body元素对象

// 获取html元素
document.documentElement // 返回html元素对象


// 点击链接弹出框
// 1 获取事件源
// 2 绑定事件 注册事件  
// div.onclick
// 3.添加事件处理程序
// div.onclick = function(){}

<a class='fa1' href="#">颜色变化</a>
<a class='fa2' href="111">颜色变化</a>
var fa1 = document.querySelector('.fa1')
// fa1.onclick = function(){alert("hhhhhh")}
fa1.onclick = ()=>{alert("aasdfasdfasd")}

// 点击button显示时间
        function times() {
            var date1 = new Date()
            return date1.getFullYear() +'-'+ (parseInt(date1.getMonth())+1 )+'-'+ date1.getDate()
        }

        var btn = document.querySelector('button');
        // var div = document.getElementsByTagName(div)[0]
        var div = document.querySelector('div')
            btn.onclick = ()=> {
                div.innerHTML = times()
            }
// 不需要点击，一直显示时间
        var div = document.querySelector('div')
        div.innerText = times();

// innerText 和 innderHtml(识别) 区别  一个不识别标签  一个识别标签
// inndertext 去除空格和换行  innerHtml w3c标准 保留空格和换行的

// 
~~~

## 自定义属性(data开头)

~~~js
<div data-index = '1'></div>
element.getAttribute('data-index'); // 获取自定义属性值
//h5新增获取自定义元素值
//dataset 是一个集合里面存放了所有data开头的自定义属性
console.log(div.dataset.index);
console.log(div.dataset['index']);
delement.setAttribute('data-index', 3); // 设置自定义属性值
~~~

## 节点操作

~~~js
element.parentNode   //获取父节点
element.childNodes   // 获取子节点(空格也算一个孩子)
//方法一
var ul = document.querySelector('ul');
for(var i = 0; i< ulchildNodes.length;i++){
    if(ul.childNodes[i].nodeType === 1){
        // ul.childNodes[i]是元素节点 ，文本节点如空格，字，nodeType=3
        console.log(ul.childNodes[i])
    }
}
// 方法二
//parentNode.childen  获取所有的子元素节点(元素)

//获取子元素第一个节点
ul.firstElementChild //ie9以下不兼容
ul.children[0]     //实际开发写法
//获取子元素最后一个节点
ul.lastElementChild   //ie9以下不兼容
ul.children[ul.children.length - 1];

//element.nextElementSibling   获取下一个兄弟节点
//element.previousElementSibling   获取下一个兄弟节点
~~~

#### 节点操作之创建和添加节点

~~~js
// 1.创建节点元素节点
var li = document.createElement('li');
// 2.添加节点 node.appendChild(child) 
var ul = document.querySelector('ul');
ul.appendChild(li);
//3.添加节点 node.insertBefore(child, 指定元素)；
var lili = document.createElement("li");
ul.insertBefore(lili, ul.children[0]);
//4.我们想要页面添加一个新的元素；1创建元素 2.添加元素

// 复制节点(克隆节点)
node.cloneNode()
ul>li$3
var ul = document.querySelector('ul');
// 1.node.cloneNode(); 括号为空号里面默认为false 浅拷贝 只复制标签不复制里面的内容
// 2.node.cloneNode(ture); 括号为true 深拷贝 复制标签里面的内容
var lili = ul.children[0].cloneNode(true);
ul.appendChild(lili)  
~~~

### 节点操作

~~~js
document.write()  // document.write("<div>111</div>") 不推荐
element.innerHTMl
document.createElement()
~~~

### DOM重点核心

~~~js
//事件监听器
var btns = document.querySelectorAll('button');
btns[1].addEventListener('click',function(){alert(22)});


//删除事件
// 传统方式删除事件
var divs = document.querySelectorAll('div');
divs[0].onclick = function(){
    alert(22);
    divs[0].onclick = null;
}

// removeEventListener 删除事件
divs[1].addEventListener('click', fn);
function fn(){
    alert(22);
    divs[1].removeEventListener('click', fn);
}
~~~

### DOM事件流（捕获-由外到内执行  冒泡-由内到外执行）

~~~js
// dom事件流三个阶段
// 1.js代码中只能执行捕获或者冒泡其中的一个阶段
// 2.onclick 和 attachEvent(ie) 只能得到冒泡阶段
// 3.捕获阶段，如果addEventListener 第三个参数是true 为捕获阶段  document->html->body->father->son
var son = document.querySelector('.son');
son.addEventListener('click',function(){
    alert('.son');
	},true);
var father = document.querySelector(".father");
father.addEventListener('click', function(){
    alert("father");
}, true);
// 当点击son盒子的时候 会先弹框father 在弹框 son
~~~

### 事件对象

~~~js
// e  element.onclick = function(e){
//			console.log(e)
//    }

e.target 和this的区别
// e.target返回的是触发事件的对象元素(点谁返回哪个元素) ， this返回的是绑定事件的对象元素
~~~

### 阻止默认行为

~~~js
// 让链接不跳转 或者让提交按钮不提交1
var a = document.querySelector('a');
a.addEventListener('click',function(e){
    e.preventDefault(); // dom标准写法
})
// 传统写法
a.onclick = function(e){
    e.preventDefault();
}

// 阻止冒泡行为
var son = document.querySelector('.son');
son.addEventListener('click',function(){
    alert('son');
    e.stopPropagation()  // 防止冒泡行为（不加会先弹框son再弹框father）
	},false);
var father = document.querySelector(".father");
father.addEventListener('click', function(){
    alert("father");
    e.stopPropagation()  // 防止冒泡行为（不加会先弹框father,要是给documen创建点击事件还会再弹框document对应的事件）
}, false);
~~~

### 事件委托

~~~js
原理：不是每一个子节点单独设置事件监听器，而是事件监听器设置在父节点上，然后利用冒泡原理影响设置每个子节点
ul>li*4  没必要循环给每个li添加事件监听
var ul = document.querySelector('ul');
ul.addEventListener('click',function(e){
    alert("addd");
    e.target.style.backgroundColor = 'pink';
})
~~~

### 禁止选中文字和禁止右键菜单

~~~js
// contextmenu 禁止右键菜单
document.addEventListener('contextmenu', function(e){
    e.preventDefault();
})
// 禁止选中文字 selectstart
document.addEventListener('selectstart', function(e){
    e.preventDefault();
})
~~~

### 鼠标点击

~~~js
document.addEventListener('click', function(e){
    // 1.client 鼠标在可视区的x和y坐标
    console.log(e.clientX);
    console.log(e.clientY);
    // 2.相当于文档页面的坐标
    console.log(e.pageX);
    console.log(e.pageY);
})
~~~

### 常见的键盘事件(onkeyup-松开；onkeydown-按下触发；onkeypress(区分大小写的)-按下时触发，但不识别功能键ctrl,shift 箭头等)

~~~js
document.onkeyup = function(e){
    console.log("我弹起了")
}
document.addEventListener("keyup", function(e){
    console.log("我弹起了")
    console.log(e.keyCode);  // 返回的ASCII码值
})

// 执行顺序 keydown -> keypress ->keyup
~~~

