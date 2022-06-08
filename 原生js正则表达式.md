# 原生js正则表达式

~~~js
// 找出字符串中的数字
var str = 'adfnasldihfo123n2knradf23r92r2h;1m';
var temp = '';
var arr [];
for(var i = 0; i<str.length;i++){
	if(str.charAt(i)>=0 && str.charAt(i)<=9){
        temp += str.charAt(i);
    }
    else{
        if(temp != ''){
			arr.push(temp);
            temp = '';
        }
    }
}
if(temp != ''){       // 情况一，全是数字；情况二，最后一个是数字
    arr.push(temp);
}
console.log(arr)

// 正则表达式
var arr = str.match(/\d+/g);

// 第一种写法
var reg = new RegExp('a');
var reg = /a/    //另外一种写法
var str = 'asdfsa';
console.log(reg.test(str));    // 返回bool值true ,代表是否匹配成功

[abcde] 匹配abcde其中任意一个
[a-Z] 匹配所有字母
[0-9] 匹配任意一个数字
/(ab)|(cd)/   匹配'ab',或者'cd'
/(a|b)cd/    匹配'acd'或者'bcd'
注意：小括号，竖括号不要放在【】内没有意义

var str = prompt();
var reg = /^a/   // 匹配以a开头的字符串
var b = reg.test(str)
console.log(b)   


// 匹配不包含a的字符
var str = prompt();
var reg = /[^a]/   // 匹配不包含a的字符
var b = reg.test(str)
console.log(b) 

// 完整匹配
var reg = /^a$/   // 只能是一个a

// 匹配数字
var reg = /\d/;

//匹配数字字母下划线
var reg = /\w/;

// 匹配空白字符
var reg = /\s/

// 匹配任意字符
var reg = /./;

// 匹配三个a连续
var reg = /a{3}/;

// 先来两个a,中间可以0-3个任意字符，后面再来一个a
var reg = /a{2}.{0,3}a/

// 数字字母下划线出现一次或一次以上
var reg = /w+/;

// ab或者cd 出现两次
var reg = /(ab|cd){2}/  // abcd abab  abab cdab

// 修饰符
var str = prompt();
var reg = new ExgExp('a', 'i');  // a 或者 A   
var reg = /a/i				// a 或者 A 
var b = reg.test(str)


//search
var str = prompt();
var reg = /\d/;
var index = str.search(reg);   // 查找字符串第一次出现数字的位置，没有返回-1


// replace
var str = prompt();
var reg = /TM|MD|MP/ig;
var str2 = str.replace(reg,'**');    // g 全局都替换(不加的话就只会替换第一次出现的)

//split

~~~

