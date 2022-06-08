# js算法

## 冒泡排序

~~~js
var a = [12, 22, 23, 54, 33, 21, 657, 2, 12, 231, 22, 1]
for (var i = 0; i < a.length - 1; i++) {
    for (var j = 0; j < a.length - i; j++)
        if (a[j] > a[j + 1]) {
            [a[j], a[j + 1]] = [a[j + 1], a[j]]
        }
}
console.log(a)
~~~

