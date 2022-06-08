# javascript

## 弹框

~~~javascript
<script>	
    prompt("弹出输入框")
</script>
~~~

## 数字类型

~~~javascript
alert(Number.MAX_VALUE); //1.7976*******
alert(Number.MIN_VALUE); // 5e-324
//infinity,表示无穷大
console.log(Number.MAX_VALUE * 2) // Infinity 
console.log(-Number.MAX_VALUE * 2) // -Infinity 无穷小
// NaN ,not a number 表示一个非数值
console.log('sss' - 100) // NaN
var a = underfined;
console.log(a + 'pink')  // unserfinedpink
consloe.log(a + 1); // NaN  underfined和数字相加，最后结果是NaN
consloe.log(a + true); // NaN  underfined和bool相加，最后结果是NaN
console.log(isNaN(12)) //false
console.log(isNaN("ss")) // true
alert(isNaN("111"))  //false  存在隐式类型转换  先调用Number(),尝试将参数转为数字类型
~~~

## 字符串

~~~js
//外双内单；外单内双。/n 表示换行符

字符串 + 数字 //字符串
var a = "12" + 12 // "1212"

字符串 + bool //字符串true/false
~~~

## null

~~~js
var b = null
console.log(b + 'pink'); //nullpink
console.log(b+1); // 1
console.log(Math.max(1,99,'pink')); //NaN
~~~

## 数据类型转换

~~~js
// 转为字符串类型 toString() String()  加号拼接字符串
Vat num = 10;
var str1 = num.toString();
var str2 = String(num);
var str3 '' + num;

//转为数值型  parseInt(string)函数；parseFloat(string)函数；Number()强制转换函数；js隐式转换(- * /)
var str = '18'
var age1 = parseInt(str); // '3.13'->3； '120px'-> 120 (开头必须是数字)
var age1 = parseFloat(str);  // '120px'-> 120   '3.14'-> 3.14
var age2 = Number(str)
console.log('12'-0); //12
console.log('12'-'10'); //2
console.log('12'*'10'); //120
console.log(18 == '18')  //true


// 转为boolean  '';0;NaN;null;underfined 这五个转为false ; 其他都转为true
var temp = Boolean('')  // false

~~~

## 加法运算

~~~js
var = 10
++a; // ++a 11 a = 11
var b = ++a + 2; // a = 12 ++a=12
console.log(b); //14

var c = 10;
c++;  //c++ 11   c 11
var d = c++ + 2; // c++  11; c 12
console.log(d);  //13

var e = 10;
var f = e++ + ++e; //e++ 10; e 11; ++e 12; e 12;
console.log(f);  22

//逻辑中断
// 如果表达式1 结果为真，结果也为真，则返回表达式2;如果表示式为假返回表达式1
console.log(123 && 456)  //456
console.log(0 && 456)     //0
// 如果表达式1 结果为真，结果也为真，则返回表达式1
console.log(123 || 456)  //123    

Var num = 10;
num += 1;  //等价于  num = num + 1；
~~~

## 三元表达式

~~~js
var num = 10;
var result = num > 5 ? 'yes' : 'no';
alert(result);  // yes
~~~

## 函数

~~~js
//如果输入的实参个数多余形参，多的实参不结束

//如果输入的实参个数小于形参，后面没有赋值的形参打印为underfined

// 有return 返回return后面的值，没有return 函数则返回underfined

// arguments
// 当前函数的内置对象。arguments对象中存储了传递的所有实参。
function fn() {
    return arguments[0]			
//返回的是类数组---1.可以.length获取长度；按照索引的方式存储；3不同于数组，没有数组的一些方法(push(),shift(),pop(),unshift(),resorve())
}
console.log(fn(1, 2, 3, 4, 5))   // 1

// 匿名函数表达式
var a = function() {
    console.log("我是匿名函数表达式")
}
a()

// var fn = function(){}，匿名函数将变量 fn提升,但调用fn()时会报错,因为fn不是函数。 （函数可以，var可以）
~~~

## 对象

~~~js
// 利用对象字面量创建对象
var obj = {
 
    sex:'男',
    sayHi:function(){
        console.log('hi~')
    }
}

// 利用new Object() 创建对象,利用等号赋值的方法添加属性和方法
var obj = new Object(); //创建一个空的对象
obj.uname = 'ah';
obj.age = 18;
obj.sayHi = function(){
    console.log('hi~')
}

//利用构造函数创建对象
// 我们需要创建四大天王的对象 相同的属性：名字，年龄，性别，相同的方法：唱歌
// 调用构造函数，必须使用new
// 只要使用new Star() 调用函数就创建一个对象
// function 构造函数名() {
//	this.属性 = 值;
//	this.方法 = function(){}
//}
//new 构造函数名();
function Star(uname,age,sex){    // 构造函数首字母大写  构造函数不需要return就可以返回结果
    
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.sing = function(sang){
        console.log('我会唱'+sang)
    }
}
// new 构造函数可以在内存中创建了一个空的对象，
// this就会指向刚才创建的这个空对象
// 执行构造函数里面的代码，给这个空对象添加属性和方法
// 返回这个对象(所以不需要return操作)
var a = new Star('刘德华','18','男')
a.sing("猪之歌")

//这种也可以
function Star(uname, age, sex, song) {    // 构造函数首字母大写  构造函数不需要return就可以返回结果

    this.name = name;
    this.age = age;
    this.sex = sex;
    this.sing = function () {
        console.log('我会唱' + song)
    }
}

var a = new Star('刘德华', '18', '男', '猪之歌')
a.sing()


// 遍历对象
var obj = {
	name:'ah',
    age:18,
    sex:'男',
    this.sing = function () {
       console.log('我会唱' + song)
    }
}
for(var i in obj){
    console.log(i,obj[i])
}
~~~

## 内置对象（Math,Date,Array,String）

### Math

~~~js
//  不需要new,不是构造函数，是静态函数，相当于全局，都可以用
max = Math.max(12,11,24)  
console.log(max)
console.log(Math.max(1,99,'pink')); //NaN
console.log(Math.max()); // -Infinity
console.log(Math.abs('-1')); // 1
console.log(Math.abs('pink')); // NaN
console.log(Math.abs('1pink')); // NaN
console.log(Math.floor('1.9')); // 1   向下取整
console.log(Math.ceil('1.1')); // 2   向上取整
console.log(Math.round('1.1')); // 2   四舍五入
console.log(Math.round('-1.5')); // -1   负数5舍6入
console.log(Math.round('-1.5')); // -1   负数5舍6入
//想要获取给定两个数之间包括自己的随机数
Math.floor(Math.random()) * (max-min+1)+min;
~~~

### Date

~~~js
// Date是一个构造函数，需要new一个对象
// .getMonth() + 1 返回的才是真正的月份，从0开始
// .getFullYear()  返回年份
// .getDate()  返回几号
// .getDay()   返回星期几  星期日返回0
var arr = new Array(); //创建一个数组对象
var obj = new Object(); //创建一个对象实例
var date = new Date()
console.log(date) //Sun Apr 17 2022 22:41:14 GMT+0800 (中国标准时间)
var date = new Date('2019-10-1 08:08')
console.log(date) //Tue Oct 01 2019 08:08:00 GMT+0800 (中国标准时间)
var date = new Date();
console.log(date.valueOf()); // 就是我们现在时间距离1970.1.1总的毫秒数
console.log(date.getTime()); //同上
// H5 新增的 获取总的毫秒数
console.log(Date.now());
~~~

#### 倒计时案例

~~~js
function conutDown(time){
    var nowTime = +new Date() // 返回的是当前时间总的毫秒数
    var inputTime = +new Date(time); //返回的是用户输入的时间总的毫秒数
    var times = (inputTime - nowTime) / 1000; //倒计时的总的秒数
    var d = parseInt(times/60/60/24);
    d = d < 10 ? '0' + d : d;
    var h = parseInt(times/60/60%24);
    var h = 10 ? '0' + h : h;
    var m = parseInt(times/60/60%60);
    var h = 10 ? '0' + m : m;
    var s = parseInt(times%60);
    var h = 10 ? '0' + s : s;
    return d + '天' + h +'时'+ m +'分'+ s + '秒'
    
}
~~~

### Array

~~~ js
// 创建数组的两个方法
// 1 通过数组字面量
var arr = [1,2,3];
console.log(arr[0])

// 2 利用new Array()创建
// var arr = new Array(); 创建一个空的数组
// var arr = new Array(2); 创建一个数组长度为2的空数组
var arr = new Array(2,3); //等价于[2,3]这种写法，里面有2个数组元素 是2 和 3
console.log(arr instanceof Array) // 返回true
console.log(Array.isArray(arr)  // 返回true
// 操作数组方法
var arr = [1,2,3];
console.log(arr.push(4,'pink')  // 返回数组长度 5
console.log(arr)  // 返回数组所有

// unshift('a')在数组开头添加一个或多个数组元素
console.log(arr.unshift('red');   // 也是返回数组长度 6
            
// pop() 删除最后一个元素
console.log(arr.pop());  // 返回被删除的最后一个元素

// shift() 删除数组的第一个元素 一次只删一个
sonsole.log(arr.shift());  //被删除的第一个元素

// reverse() 翻转数组
arr.reverse();

// sort() 排序 ,本身有bug [1,13,2].sort()->[1,13,2]
r.sort();
arr.sort(function(a,b){
    return a- b; //升序排序
    // return b - a  //降序排序
}
        
// indexOf() 返回数组的索引号 (只返回第一个满足参数的索引；数组没有返回 -1)
// lastIndexOf 返回数组的索引号 (只返回第一个满足参数的索引；数组没有返回 -1) 从后遍历
         
// 数组去重
function unique(arr){
    var newArr = [];
    for(var i = 0; i < arr.length; i++){
        if(newArr.indexOf(arr[i]) === -1) {
            newArr.push(arr[i];
			}
    }
    return newArr;
}


~~~

### string

~~~js
// toString() 将数组转为字符串
// join('-')  用-符号分割数组的每个元素成为字符串

// 字符串不可变 只是重新申请一个内存
var str = "改革春风吹满面";
console.log(str.indexOf('春')); //2
console.log(str.indexOf('春',3)); //5  // 从索引3开始找

案例
// 查找"adfhawdufhauewakjsdfddadtshsf"中所有f出现的次数和位置
var a = "adfhawdufhauewakjsdfddadtshsf";
var index = str.indexOf('o');
while(index !== -1){
    console.log(index);
    console.log(a[index])
    index = str.indexOf('o',index++);
}

//返回索引对应的字符
charAt(index) 根据位置返回字符
var str = 'andy';
console.log(str.charAt(3)) // y

// str[index]
var str = 'andy';
console.log(str[3]) // y

// charCodeAt(index) 返回相应索引号的字符ASCII值，目的：判断用户按下了哪个键
console.log(str.charCodeAt(0); // 97
            
// 判断一个字符串各个字母出现的个数
 var o = {}
var a = 'eifhosidhfwehqapuhfamdasldhgqiwaewroqqabsaaaweasafg';  
for (var  i = 0; i < a.length; i++){
    var chars = a.charAt(i);
    if (o[chars]){
        o[chars] = o[chars] + 1;
    }
    else{
        o[chars] = 1;
    }
}
console.log(o)

// 将字符串里的一个字母所有替换成另外一个字母
var str = 'abcdsdsdsaa';  

while (str.indexOf('o') !== -1) {
    str = str.replace('o', '*')
}

// 将字符串变成数组
var str = 'red,pknd,buss';
var a = str.split(','); // a 是一  个数组
~~~

### 基本数据类型（栈）

#### string;  number ; boolean;  underfined ;null; symbol  



### 引用数据类型（堆）

#### 

### 