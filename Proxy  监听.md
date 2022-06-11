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





![image-20220609000842395](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220609000842395.png)





## 监听in的捕获器

![image-20220609001155791](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220609001155791.png)



## delete捕获器

![image-20220609001249791](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220609001249791.png)





## 13种——捕获器

![image-20220609001915375](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220609001915375.png)





## apply调用和new调用

![image-20220609002405608](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220609002405608.png)





![image-20220609001915375](C:\Users\root\Desktop\1.png)



## Proxy和Reflect结合使用

~~~js
obj  = {
    name: 'cobe',
    age: 18
}
const objProxy = new Proxy(obj, {
    get: function(target, key, receiver){
        console.log("获取值---------------------")
        console.log(`监听${key}的值为${target[key]}`, target)
        return Reflect.get(target, key)
    },
    set:function(target,key,newValue, receiver){
        console.log("设置值------------------")
        // 和直接用 target[key] = newValue 设置值 的区别是不会直接操作obj 
        // 区别2：object.freeze(target)设置后，target[key] = newValue就不会起作用，我们不能感知
        // const result = Reflect.get(target,key, newValue)  会返回一个bool值，可以感知是否设置成功
        Reflect.get(target,key, newValue)
    }
})
objProxy.name = 'code';
console.log(objProxy.name)



[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
设置值------------------
获取值---------------------
监听name的值为cobe { name: 'cobe', age: 18 }
cobe

[Done] exited with code=0 in 0.099 seconds

~~~





## obj里的this指向 其实下面的例子没有做到代理_name的作用，直接可以调用get 里的name方法获取__name了

~~~js
const obj  = {
    _name: 'cobe',  // 私有属性
    age: 18,
    get name(){
        return this._name // 此时的this指向obj ,因为要是指向objProxy的化，会再次访问objProxy里的get方法再次打印
    },

    set name(newValue){
        this._name = newValue
    }
};

const objProxy = new Proxy(obj,{
    get: function(target,key, receiver){
        console.log("监听获取值-----------------")
        console.log("receiver代理对象:",receiver)
        console.log("代理对象就是objProxy", receiver === objProxy)
        return Reflect.get(target,key)
    },
    set:function(target,key,newValue, receiver){
        console.log("监听设置值--------------------")
        console.log("receiver代理对象:",receiver)
        console.log("代理对象就是objProxy", receiver === objProxy)
        Reflect.set(target,key,newValue)
    }
});
console.log(objProxy.name);
console.log(objProxy._name);
objProxy.name = 'cwhy';
console.log(objProxy.name);
console.log(objProxy._name);


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
监听获取值-----------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cobe
监听获取值-----------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cobe
监听设置值--------------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
监听获取值-----------------
receiver代理对象: { _name: 'cwhy', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cwhy
监听获取值-----------------
receiver代理对象: { _name: 'cwhy', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cwhy

~~~



## 解决上面的例子this不是指向代理，指向obj的问题导致直接访问obj的问题，添加 receiver参数

~~~js
const obj  = {
    _name: 'cobe',  // 私有属性
    age: 18,
    get name(){
        return this._name // 此时的this指向obj ,因为要是指向objProxy的化，会再次访问objProxy里的get方法再次打印
    },

    set name(newValue){
        this._name = newValue
    }
};

const objProxy = new Proxy(obj,{
    get: function(target,key, receiver){
        console.log("监听获取值-----------------")
        console.log("receiver代理对象:",receiver)
        console.log("代理对象就是objProxy", receiver === objProxy)
        return Reflect.get(target,key,receiver)
    },
    set:function(target,key,newValue, receiver){
        console.log("监听设置值--------------------")
        console.log("receiver代理对象:",receiver)
        console.log("代理对象就是objProxy", receiver === objProxy)
        Reflect.set(target,key,newValue,receiver)
    }
});
console.log(objProxy.name);
console.log(objProxy._name);
objProxy.name = 'cwhy';
console.log(objProxy.name);
console.log(objProxy._name);


[Running] node "c:\Users\root\Desktop\静态页+静态组件\todoList\todolist\Peflect.js"
监听获取值-----------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
监听获取值-----------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cobe
监听获取值-----------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cobe
监听设置值--------------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
监听设置值--------------------
receiver代理对象: { _name: 'cobe', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
监听获取值-----------------
receiver代理对象: { _name: 'cwhy', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
监听获取值-----------------
receiver代理对象: { _name: 'cwhy', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cwhy
监听获取值-----------------
receiver代理对象: { _name: 'cwhy', age: 18, name: [Getter/Setter] }
代理对象就是objProxy true
cwhy

[Done] exited with code=0 in 0.268 seconds
~~~





## Reflect中construct作用

