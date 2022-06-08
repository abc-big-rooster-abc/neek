# BOM

window ->(document  location  navigation screen history)

## 窗口加载事件

~~~js
window.onload = function(){
}
// 或者
// window.onload是窗口（页面）加载事件。当文档内容完全加载完成会触发该事件(包括图像，脚本文件，css文件等)，就调用的处理函数
window.addEventListener("load",function(){
    
})

// DOMContentLoaded 是DOM加载完毕，不包含图片falsh, css等等就可以执行，加载速度比load加载快
document.addEventListener('DOMContentLoaded', function(){})

~~~

## 定时器

### setTimeout() 定时器

~~~js
window.setTimeout(调用函数, [延迟毫秒数]); // window 可以省略不写
setTimeout(function(){}, 2000);  // 到了两秒执行参数一的函数
// 这个调用函数可以直接写函数，也可以直接写函数名
function calback(){
		console.log("爆炸")
	}
setTimeout(calback, 4000);

// 案例：广告五秒之后关闭
var ad = documrnt.querySelector('.ad');
setTimeout(function(){
    ad.styel.display = "none";
},5000);
~~~

### 清除定时器clearTimeout

~~~js
<button>点击停止定时器</button>
var btn = document.querySelector('button');
var timer = setTimeout(function(){   //仅仅给定时器起一个名字，为了后面的清除定时器做准备
    console.log("爆炸了")
},5000);
btn.addEventListener('click', function(){
    clearTimeout(timer);
})
~~~

### 定时器setInterval  每隔一段时间就会执行

~~~js
<button>点击停止定时器</button>
var btn = document.querySelector('button');
var timer = setInterval(function(){   //仅仅给定时器起一个名字，为了后面的清除定时器做准备
    console.log("每个隔5秒爆炸")
},5000);
btn.addEventListener('click', function(){
    clearInterval(timer);
}) 
~~~

## 同步和异步(同步执行完再执行异步)

~~~js
// js的异步是通过回调函数实现的 ，一般而言，异步任务有以下三种类型
// 1.普通事件，如click resize 等
// 2.资源加载，如load ,error等
// 3.定时器，包括setInterval、setTimeout 等
~~~

## location对象

~~~js
window对象给我们提供了一个location属性用于获取或设置窗体的url ,并且可以用于解析url。因为这个属性返回的是一个对象，所以我们称为location对象

location.href  // 获取或者设置 整个URL
location.search // 返回参数
location.assign('http://www.baidu.com'); // 可以回退功能，回退上一个网址
location.replace('http://www.baidu.com'); // 不记录历史，不可以后退
location.reload();  // 重新刷新界面
~~~

## navigator 对象  （获取浏览器信息，可以判断是移动端还是网页端，）

## history对象

~~~js
history.back();  // 可以后退功能
history.forward(); // 前进功能
history.go(参数)；  // 前进后退功能，参数如果是1，前进一个页面 如果是-1后退一个页面
~~~

## offsetLeft和offsetTop获取元素偏移

~~~js
// 想获取子元素距离父元素的偏移，需要对父元素加上一个定位如 position:relative
var father = document.querySelector('.father');
var father = document.querySelector('.son');
console.log(father.offsetTop); // 距离网页顶部距离
console.log(father.offsetLeft);
console.log(father.offsetWidth);  // 获取盒子的宽度
console.log(father.offsetHeight);  // 获取盒子的高度
~~~

## offset(获取元素大小用) 和style(修改元素大小使用)区别

~~~js
// 都可以获取盒子的宽度和高度
// 区别在于style只能获取行内设置的宽度和高度，通过css设置的宽度和高度则获取不了  ，而offset可以
.father {
    w:500px;
    h:500px
}
console.log(father.offsetWidth);  // 打印500  但是只能读，不可以改变大小
console.log(father.style.width);  // 没有打印
~~~

## client (clientWidth和offsetWidth区别-clientWidth不带边框宽度)

~~~js
element.clientTop  //返回元素上边框的大小
~~~

## mouseover 和 mouseenter 区别

~~~js
当鼠标移动到元素上就会触发mouseenter事件
类似于mouseover,他们两者之间的差别是
mouseover 鼠标经过自身盒子会触发，经过子盒子也会触发，mouseenter 只会经过自身盒子触发
mouseenter不会冒泡；mouseover会，在经过子盒子没有触发之后，会冒泡到父盒子
mouseenter <=> mouseleave
~~~

