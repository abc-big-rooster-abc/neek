# ES6语法

## 数组API

~~~js
// 数组API
//forEach  只是一个单纯的遍历
var arr = [1,2,3,4,5,6,7];
arr.forEach(function (item,index){
		console.log(item, index);
	})

// map  遍历数组的同时每一次遍历返回一个值，所有的返回值构成一个新的数组
var arr1 = arr.map(function(item,index){
    console.log(index, item);
    return item * 2;
})

// some 遍历数组，每一次遍历的时候返回一个条件，返回是bool 只要有一次返回true,就返回true
var isEven = arr.some(function(item, index){
    console.log(item, index);
    return item % 2 == 0;
})
console.log(isEven); // true   


// every 遍历数组，每一次遍历的时候返回一个条件，返回是bool 只有全部返回true,就才返回true
var isEven = arr.some(function(item, index){
    console.log(item, index);
    return item % 2 == 0;
})
console.log(isEven); // false  


// reduce  归并
var sum = arr.reduce(function(res, current){
    // 第一次遍历的返回值会作为第二次的res使用
    return res + current;
});
console.log(sum); 

// 在后面给一个初始值结果比不给初始值多10
var sum1 = arr.reduce(function(res, current){
    // 第一次遍历的返回值会作为第二次的res使用
    return res + current;
},10);
console.log(sum1);  


// includes  数组里包含某个值就得到true 不包含就false  indexOf() 返回索引，没有返回-1
console.log(arr.includes(18))
~~~

## 字符串API

~~~js
// includes
var str = 'aksdnfoaie';
console.log(str.includes('a'));   // true

// startsWith
// endsWith
console.log(str.startsWith('e'));  // false
console.log(str.endsWith('e'))   //true

// trim 去除前后空格
var str = '  sfs dw ';
var str1 = str.trim();
console.log(str1);  //sfs dw
~~~

## 对象API

~~~js
// defineProperty  // 给对象定义属性
var obj = {};
Object.defineProperty(obj,'name',{
    value:'Dary,
    enumerable:false,  // 是否可枚举(只要能for。。。in 遍历到的属性都是可枚举的）  默认为true
    writable:false,     // 定义是否可以改写，false不可以被修改
})



// assign  assign做的是浅克隆
let obj1 = {
  m: 1,
  n: 2,
  attr: {
    name: 'Jack',
    age: 18
  }
}
 
let obj2 = Object.assign({}, obj1);
 
obj1.attr.name = 'Tom';
console.log( obj1.attr.name );  // Tom
console.log( obj2.attr.name );  // Tom
 
obj2.attr.name = 'Jarry';
console.log( obj1.attr.name );  // Jarry
console.log( obj2.attr.name );  // Jarry

~~~

## 箭头函数

~~~js
// 箭头函数定义必须要在调用之前 和let const 使用相似
var fn = () => {
}                     // 等同于 var fn = function(){}

~~~

## 结构赋值

~~~js
var arr = [23,45,6];
// 按顺序 把数组的值赋值给abc三个变量
var [a,b,c] = arr;   // var a = arr[0], b= arr[1], c= arr[2];


~~~

## 扩展运算符

~~~js
var arr = [323,2345,234];
var fn = (x,y,z) => {
    console.log(x+y+z)
}
fn(arr[0],arr[1],arr[2]);

// ...的意思是把数组展开成一组用逗号隔开的值...arr 等于 322，2345，234
fn(...arr);

// ...的作用是双向的
// 把调用fn1的时候传递过来的所有参数合并到arr这个数组里
var fn1 =(...arr){             // 求和
    console.log(arr)  // 是一个数组
    var sum = arr.reduce((res,current) => {
        return res + current
    })
    console.log(sum)
    
};
fn1(1,3,4);

~~~

## 模板字符串

~~~js
var html = `<li>姓名：<b>${obj.name}</b><li>
			<li>年龄：<b>${obj.age}</b></li>`
// 等同于
var html = '<li>姓名：<b>' + obj.name + '</b><li>' +
			'<li>年龄：<b>' + obj.age + '</b></li>'

document.getElementById('list').innerHTML = html;
~~~

## 函数默认值

~~~js
fn  (a,b,c=0) => {
    
   console.log(a+b+c);
}
fn(1,3)
~~~

# 面试题

## 作用域问题 AO GO理解

~~~js
var a=b=10;  // 等同于 var a = 10; b= 10;
~~~



![image-20220506194705062](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220506194705062.png)

![image-20220506200911315](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220506200911315.png)

![image-20220506204600361](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220506204600361.png)

## 闭包

![image-20220506234612517](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220506234612517.png)

### 总结；当闭包执行完函数return的时候，最外层函数执行完毕，对应的AO就会自动销毁，不指向AO对象，之所以 最内层的函数，还可以访问上一层变量的原因是，最内层的地址存放在GO(全局内)，通过执行fn(),可以找到最内层的AO对象，而最内层的函数内部的parentScope指向最外层函数，所以最外层函数没有销毁，这是可以访问到外层函数变量的原因；要想解决闭包，执行之后，将 fn = null ,让GO里的fn地址指向0x00(空）；虽然最内层函数parentScope还指向外层函数，但根节点没有指向最内层函数。

![image-20220507004055068](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220507004055068.png)

# this 指向问题面试

## 内置函数要求我们传入一个函数，至于这个函数的this指向谁，我们是不知道的，得看内部实现执行这个传入函数的执行方式，直接执行就指向window,隐式执行就指向调用的对象

![image-20220508093643806](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508093643806.png)

## this 显示绑定优先级大于隐士绑定

![image-20220508094805435](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508094805435.png)

## new的优先级高于显示绑定

![image-20220508095422409](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508095422409.png)

## 箭头函数

![image-20220508102137019](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508102137019.png)

## 单行箭头函数想返回一个对象写法

![image-20220508103055779](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508103055779.png)

## 箭头函数没有this指向，他会找他的父级

![image-20220508104308105](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508104308105.png)

![image-20220508104420874](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508104420874.png)

## 面试题1

![image-20220508105031404](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508105031404.png)

![](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508105503566.png)



## person1.foo3.call(person2) 是指向persion2的，没错。但执行的时候是独立函数调用所以指向window



![image-20220508105749786](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508105749786.png)









![image-20220508105854420](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508105854420.png)

## 面试题3

![image-20220508111247608](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508111247608.png)

![image-20220508111458469](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508111458469.png)

![image-20220508111552462](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508111552462.png)

![image-20220508111729455](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508111729455.png)

![image-20220508112623628](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508112623628.png)

![image-20220508112940745](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508112940745.png)

# 面试题实现call函数功能

## 1.载函数的prototype上构建函数；2.thisArg 为改变this指向的值，...args为函数传入的参数（...可以接受多个参数）；3. var fn = this;在调用hycall时用的式隐士绑定(fn.hycall()),可以获取被执行的函数， 4 如果传入的this指向一个number,不可以使用thisArg.fn = fn;

## 如果传入的是null ,underfined;在call函数里会将this指向window,所以第9行做了判断；5.改变this指向thisArg(第12行)；6.执行函数，（...args）利用扩展运算符，将形参以数组形式 分离

### 补充：第九行判断当thisArg传入0的时候因该指向number(0) :优化

![image-20220508174016567](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508174016567.png)

![image-20220508160035048](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508160035048.png![image-20220508161404213](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508161404213.png)

## 实现apply功能

![image-20220508171152363](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508171152363.png)

### 当不传入参数的时候会报错，所以有了上面12-16行的代码( 13行没有...argArray),还有其他两种写法方式

![image-20220508171556143](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508171556143.png)

## bind代码实现

![image-20220508175613305](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508175613305.png)

![image-20220508175748498](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508175748498.png)

# arguments

![image-20220508185111792](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508185111792.png)

## arguments类数组转为数组，4种方法

![image-20220508190649407](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508190649407.png)

![image-20220508191711496](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508191711496.png)

## array中的slice实现

![image-20220508190949908](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508190949908.png)

## ES6对多形参的处理，num1=10; num2=20; args=[30,40,50]

![image-20220508193331693](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508193331693.png)

# 纯函数

## 数组切分方式

![image-20220508215159353](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508215159353.png)

# 柯里化写法

![image-20220508222709340](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508222709340.png)

## 简写柯里化

![image-20220508222823086](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508222823086.png)

![image-20220508225737135](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220508225737135.png)

# eval函数

![image-20220509195249742](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220509195249742.png)

# defineProperty

![image-20220509205130474](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220509205130474.png)

![image-20220509205752680](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220509205752680.png)

![image-20220509211238767](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220509211238767.png)

# 构造函数执行过程

![image-20220510223909455](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510223909455.png)

# 隐式原型

![image-20220510230538546](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510230538546.png)

![image-20220510231034057](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510231034057.png)  

# 显式原型prototype,函数特有

![image-20220510231623776](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510231623776.png)

![image-20220510231808706](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510231808706.png)

![image-20220510232557079](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510232557079.png)

![image-20220510233204532](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510233204532.png)

![image-20220510234041421](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510234041421.png)

## 修改prototype

### constructor 指向foo函数（有点缺陷，真实的prototype是不可以遍历得到constructor）

![image-20220510235042659](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510235042659.png)

![image-20220510235224523](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510235224523.png)

### 修改constructor办法

![image-20220510235306546](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220510235306546.png)



### 案例

![image-20220511000120726](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511000120726.png)

![image-20220511000023716](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511000023716.png)

# 原型链

![image-20220511203506156](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511203506156.png)

# 原型链继承（弊端：new Person() 如果person里有参数的话，会设置为underfiend,增加内存损耗 ）

# 实际效果图：缺点就是每次创建一个新对象的时候都会实例一些不必要的underfined值（this.name = underfined）（因为使用new Person()方法创建新的对象）

## ![image-20220514103837040](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514103837040.png) 

![image-20220511210624852](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511210624852.png)

![image-20220511210843477](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511210843477.png)

![image-20220511210652174](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511210652174.png)

## 继承弊端

![image-20220511212306541](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511212306541.png)

![image-20220511212448357](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511212448357.png)

## （弊端：Person.call 如果person里有参数的话，会设置为underfiend,增加内存损耗 ）

![image-20220511213820735](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220511213820735.png)

# 原型式继承（对象继承对象）

![image-20220513232319532](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220513232319532.png)

![image-20220513232541583](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220513232541583.png)

## 弊端：

![image-20220514103412510](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514103412510.png)

# 寄生式继承

![image-20220514140725974](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514140725974.png)

![image-20220514141801464](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514141801464.png)

# 最终实现继承，避免重复调用父类赋值underfined

![image-20220514143848170](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514143848170.png)

![image-20220514143958921](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514143958921.png)

# hasOwnProperty

![image-20220514144708699](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514144708699.png)

![image-20220514144832427](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514144832427.png)

# instanceof

![image-20220514145905556](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514145905556.png)

# isPrototypeOf

![image-20220514151004443](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514151004443.png)

![image-20220514150758575](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514150758575.png)





![image-20220514155839116](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514155839116.png)

![image-20220514152626518](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514152626518.png)

![image-20220514161341890](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514161341890.png)

![image-20220514162930458](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514162930458.png)

![image-20220514163818853](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514163818853.png)

![image-20220514164135728](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514164135728.png)

# class

![image-20220514174819450](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514174819450.png)

![image-20220514175355268](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514175355268.png)





![image-20220514175758358](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514175758358.png)

![image-20220514175709861](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514175709861.png)



# class 继承

![image-20220514182340587](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514182340587.png)

# 重写父类的方法，直接父类方法名重写；在父类方法的基础上加内容

![image-20220514183438918](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220514183438918.png)