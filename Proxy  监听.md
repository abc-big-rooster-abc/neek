# Proxy  监听

## 之前监听可以用defineProperty

~~~js
const obj = {
    name: 'why',
    age: 18
}
Object.defineProperty(obj, 'name', {
    get: function(){
        console.log("监听到obj对象的name属性被访问了")
    }，
    set: function(){
    console.log("监听到obj对象的name属性被设置值")
}
    
})
console.log(obj.name)
obj.name = 'jaj'
~~~

![image-20220608230127160](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608230127160.png)

## 监听对象里的所有

~~~js
const obj = {
    name: 'why',
    age: 18
}
Object.key(obj).forEach(key => {
    let value = obj[key];
    Object.defineProperty(obj, key, {
        get: function(){
            console.log(`监听到obj对象的${key}属性被访问了`);
            return value
        }，
        set: function(newValue){
        console.log(`监听到obj对象的${key}属性被设置值`)
        value = newValue
    	}

    })
})
obj.name = 'kobe';
obj.age = 30;
console.log(obj.name);
console.log(obj.age)

~~~

![image-20220608231412095](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608231412095.png)

## defineProperty缺点

![image-20220608231523899](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608231523899.png)









# Proxy

![image-20220608233042090](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608233042090.png)

~~~js
const  obj = {
    name: 'why',
    age: 18
}

const objProxy = new Proxy(obj,{})
console.log(objProxy.name)
console.log(objProxy.age)
objProxy.name = 'kobe'
objProxy.age = 30
console.log(obj.name)
console.log(obj.age)
~~~

![image-20220608235431134](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608235431134.png)

## Proxy实现事件监听

![image-20220609000040332](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220609000040332.png)