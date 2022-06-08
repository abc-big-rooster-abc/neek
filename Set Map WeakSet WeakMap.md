# Set Map WeakSet WeakMap

## es6之前存储数据的结构主要两种：数组，对象

## 新增另外两种数据结构：Set Map 以及他们的另外形式WeakSet WeakMap

# Set(和python里的元组有点像不能重复）

![image-20220607233253596](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220607233253596.png)

~~~js
// 数组去重
const arr = [33,12,12,22,32];
const arr_1 = new Set(arr);
const newArr = Array.from(arr_1);
//或者展开运算符
const newArr = [...arr_1]
~~~

## 属性size

arr_1.size

## 方法 .add()   .delete(数值）  .has(33)返回boolZ值    .clear()  清除整个set

![image-20220607234549297](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220607234549297.png)



# WeakSet

![image-20220608000538493](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608000538493.png)

![image-20220608000730874](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608000730874.png)

## ![image-20220607235341402](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220607235341402.png)

## WeakSet和Set 弱引用和强引用理解

### 强引用（就算 obj = null 0x100也不会被销毁）

![image-20220608000004993](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608000004993.png)

# Map

![image-20220608201202028](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608201202028.png)

## 对象不可以作为对象的key 否则会被解析成字符串'[object object]'

![image-20220608201602775](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608201602775.png)

## Map 可以对象属性作为key

![image-20220608203019159](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203019159.png)

## Map 属性和方法

![image-20220608203303351](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203303351.png)

![image-20220608203417835](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203417835.png)

![image-20220608203452323](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203452323.png)

## Map遍历

![image-20220608203706556](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203706556.png)

![image-20220608203742739](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203742739.png)

## 两种方法效果一样 解构运算符

![image-20220608203858399](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203858399.png)

![image-20220608203754187](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203754187.png)

![image-20220608203805360](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608203805360.png)

# WeakMap

![image-20220608205518464](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608205518464.png)

![image-20220608211138838](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608211138838.png)

# 4.应用场景（vue3响应式原理）用weakMap的原因是如果有天想对对象进行销毁，希望真正销毁（弱引用）

![image-20220608213618164](C:\Users\root\AppData\Roaming\Typora\typora-user-images\image-20220608213618164.png)