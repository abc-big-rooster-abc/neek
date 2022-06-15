# Storage

## WebAtorage主要提供一种机制，可以让浏览器提供一种比cookie更直观的key,value存储方式

## localStorage:本地存储，提供的是一种永久性的存储方式，在关闭浏览器重新打开时，依旧保留

## sessionStorage:会话存储，提供的是本次会话的存储，关闭会话时，存储被清除

## 

## localStorage方法

~~~js
localStorage.setItem("name","coderwhy")
localStorage.setItem("age",18)

// length
console.log(localStorage.length)
for(let i = 0; i<localStorage.length;i++){
    const key = localStorage.key(i)
    console.log("key:",key)
    console.log(localStorage.getItem(key))
    
}

// 3 .key方法

// getItem(key)
console.log(localStorage.getItem("age"))

// removeItem
localStorage.removeItem("age")
console.log(localStorage.getItem("age"))

// clear方法
localStorage.clear()


2
Peflect.js:8 key: age
Peflect.js:9 18
Peflect.js:8 key: name
Peflect.js:9 coderwhy
Peflect.js:16 18
Peflect.js:20 null
~~~

## 分装

~~~js
class MyCache{
    constructor(isLocal = true){
        this.storage = isLocal? localStorage: sessionStorage 
    }

    setItem(key,value){
        if(value){
            this.storage.setItem(key, JSON.stringify(value))
        }
        
    };
    getItem(key){
        let value = this.storage.getItem(key)
        if(value){
            value = JSON.parse(value)
            return value
        }
    };

    removeItem(key){
        this.storage.removeItem(key)
    };

    clear(){
        this.storage.clear()
    }


}
localStorage_0 = new MyCache();
sessionStorage_0 = new MyCache(false);
export {
    localStorage_0,
    sessionStorage_0
}

~~~

