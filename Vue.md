# Vue

## vue的生命周期

~~~js
getFullName(){} 等同于  getFullName: function(){} 
~~~

## 计算属性（computed）

~~~js
<h2>{{fullName}}</h2>      // 不需要写成fullName() ,直接写fullName就可以调用
<script>
    data: {
        firstName: 'xie',
        lastName: 'gongsheng'
    }
    computed:{
        fullName: function(){
            return this.fistName + ' ' + this,lastName,
        }
    }
</script>
~~~

